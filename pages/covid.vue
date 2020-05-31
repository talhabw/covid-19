<template>
  <v-container>
    <v-row justify="center">
      <v-col cols="12" sm="6" md="4">
        <v-card elevation="20">
          <v-card-title class="headline red--text text--darken-4">
            <v-spacer />
            TOTAL CASES
            <v-spacer />
          </v-card-title>
          <v-card-text class="display-1 text-center red--text text--accent-3">
            {{ total.cases }}
          </v-card-text>
        </v-card>
      </v-col>
      <v-col cols="12" sm="6" md="4">
        <v-card elevation="20">
          <v-card-title class="headline red--text text--darken-4">
            <v-spacer />
            TOTAL DEATHS
            <v-spacer />
          </v-card-title>
          <v-card-text class="display-1 text-center red--text text--accent-3">
            {{ total.deaths }}
          </v-card-text>
        </v-card>
      </v-col>
      <v-col cols="12" sm="6" md="4">
        <v-card elevation="20">
          <v-card-title class="headline red--text text--darken-4">
            <v-spacer />
            TOTAL RECOVERED
            <v-spacer />
          </v-card-title>
          <v-card-text class="display-1 text-center red--text text--accent-3">
            {{ total.recovered }}
          </v-card-text>
        </v-card>
      </v-col>
      <v-col cols="12" sm="6" md="4">
        <v-card elevation="20">
          <v-card-title class="headline red--text text--darken-4">
            <v-spacer />
            NEW CASES
            <v-spacer />
          </v-card-title>
          <v-card-text class="display-1 text-center red--text text--accent-3">
            {{ total.todayCases }}
          </v-card-text>
        </v-card>
      </v-col>
      <v-col cols="12" sm="6" md="4">
        <v-card elevation="20">
          <v-card-title class="headline red--text text--darken-4">
            <v-spacer />
            NEW DEATHS
            <v-spacer />
          </v-card-title>
          <v-card-text class="display-1 text-center red--text text--accent-3">
            {{ total.todayDeaths }}
          </v-card-text>
        </v-card>
      </v-col>
      <v-col cols="12" sm="6" md="4">
        <v-card elevation="20">
          <v-card-title class="headline red--text text--darken-4">
            <v-spacer />
            ACTIVE CASES
            <v-spacer />
          </v-card-title>
          <v-card-text class="display-1 text-center red--text text--accent-3">
            {{ total.active }}
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
    <v-row justify="center">
      <v-col cols="12">
        <v-text-field
          v-model="search"
          label="SEARCH"
          prepend-inner-icon="search"
          outlined
          rounded
          clearable
          clear-icon="backspace"
        ></v-text-field>
      </v-col>
    </v-row>
    <v-data-iterator
      :items="items"
      :items-per-page.sync="itemsPerPage"
      :page="page"
      :search="search"
      :sort-by="sortBy"
      :sort-desc="sortDesc"
      hide-default-footer
    >
      <template v-if="isMobile" v-slot:header>
        <v-toolbar color="indigod3" class="mb-1" dark>
          <template>
            <v-select
              v-model="sortBy"
              background-color="indigol1"
              color="indigol3"
              item-color="red darken-1"
              flat
              solo-inverted
              hide-details
              class="text-uppercase"
              :items="keys"
              prepend-inner-icon="search"
              label="Sort by"
            ></v-select>
            <v-spacer />
            <v-btn-toggle v-model="sortDesc" mandatory>
              <v-btn large depressed color="indigol1" :value="false">
                <v-icon>mdi-arrow-up</v-icon>
              </v-btn>
              <v-btn large depressed color="indigol1" :value="true">
                <v-icon>mdi-arrow-down</v-icon>
              </v-btn>
            </v-btn-toggle>
          </template>
        </v-toolbar>
      </template>

      <template v-slot:default="props">
        <v-row>
          <v-col
            v-for="item in props.items"
            :key="item.country"
            cols="12"
            sm="6"
            md="4"
            lg="3"
          >
            <v-card>
              <v-card-title class="subheading font-weight-bold">{{
                item.country
              }}</v-card-title>

              <v-divider></v-divider>

              <v-list dense>
                <v-list-item v-for="(key, index) in filteredKeys" :key="index">
                  <v-list-item-content
                    :class="{
                      'indigo--text text--lighten3': sortBy === key
                    }"
                    >{{ key.toUpperCase() }}:</v-list-item-content
                  >
                  <v-list-item-content
                    class="align-end"
                    :class="{
                      'indigo--text text--lighten3': sortBy === key
                    }"
                    >{{ item[key] }}</v-list-item-content
                  >
                </v-list-item>
              </v-list>
            </v-card>
          </v-col>
        </v-row>
      </template>

      <template v-slot:footer>
        <v-row class="mt-2" align="center" justify="center">
          <span class="grey--text">Items per page</span>
          <v-menu offset-y>
            <template v-slot:activator="{ on }">
              <v-btn dark text color="primary" class="ml-2" v-on="on">
                {{ itemsPerPage }}
                <v-icon>mdi-chevron-down</v-icon>
              </v-btn>
            </template>
            <v-list>
              <v-list-item
                v-for="(number, index) in itemsPerPageArray"
                :key="index"
                @click="updateItemsPerPage(number)"
              >
                <v-list-item-title>{{ number }}</v-list-item-title>
              </v-list-item>
            </v-list>
          </v-menu>

          <v-spacer></v-spacer>

          <span
            class="mr-4
            grey--text"
          >
            Page {{ page }} of {{ numberOfPages }}
          </span>
          <v-btn
            fab
            dark
            color="blue darken-3"
            class="mr-1"
            @click="formerPage"
          >
            <v-icon>mdi-chevron-left</v-icon>
          </v-btn>
          <v-btn fab dark color="blue darken-3" class="ml-1" @click="nextPage">
            <v-icon>mdi-chevron-right</v-icon>
          </v-btn>
        </v-row>
      </template>
    </v-data-iterator>
  </v-container>
</template>

<script>
import axios from "axios"
export default {
  async asyncData() {
    const config = {
      headers: {
        "Content-Type": "application/json;charset=UTF-8"
      }
    }

    const total = await axios.get(
      `https://disease.sh/v2/all?yesterday=false&allowNull=false`,
      config
    )
    const country = await axios.get(
      `https://disease.sh/v2/countries?yesterday=true&allowNull=false`,
      config
    )

    return { total: total.data, items: country.data }
  },
  data() {
    return {
      itemsPerPageArray: [4, 12, 18],
      search: "",
      filter: {},
      sortDesc: false,
      page: 1,
      itemsPerPage: 12,
      sortBy: "country",
      keys: [
        "cases",
        "todayCases",
        "deaths",
        "todayDeaths",
        "recovered",
        "active",
        "tests"
      ]
    }
  },
  computed: {
    theme() {
      return this.$vuetify.theme.dark
    },
    numberOfPages() {
      return Math.ceil(this.items.length / this.itemsPerPage)
    },
    filteredKeys() {
      return this.keys.filter(key => key !== `Name`)
    },
    isMobile() {
      return this.$vuetify.breakpoint.smAndUp
    }
  },
  methods: {
    nextPage() {
      if (this.page + 1 <= this.numberOfPages) this.page += 1
    },
    formerPage() {
      if (this.page - 1 >= 1) this.page -= 1
    },
    updateItemsPerPage(number) {
      this.itemsPerPage = number
    }
  }
}
</script>
