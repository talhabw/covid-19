<template>
  <div>
    <v-navigation-drawer
      v-model="drawer"
      color="indigod3"
      clipped
      app
      fixed
      dark
    >
      <v-list>
        <v-list-item v-for="(item, i) in items" :key="i" :to="item.to" exact>
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title" />
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <!-- ------------------------- -->
    <v-app-bar
      color="indigod3"
      :collapse-on-scroll="drawer === false ? collapsed : !collapsed"
      :clipped-left="true"
      :collapse="drawer === false ? collapsed : !collapsed"
      fixed
      app
      dark
    >
      <v-app-bar-nav-icon @click="drawer = !drawer" />
      <v-spacer />
      <v-icon color="white" @click="changeTheme">mdi-theme-light-dark </v-icon>
    </v-app-bar>
  </div>
</template>

<script>
export default {
  data() {
    return {
      theme: false,
      collapsed: true,
      drawer: false,
      items: [
        {
          icon: "mdi-apps",
          title: "Home",
          to: "/"
        },
        {
          icon: "extension",
          title: "Covid-19 App",
          to: "/covid"
        }
      ]
    }
  },
  methods: {
    changeTheme() {
      this.theme = !this.theme
      this.$vuetify.theme.dark = this.theme
    }
  }
}
</script>

<style></style>
