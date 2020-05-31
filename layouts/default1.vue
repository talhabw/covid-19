<template>
  <v-app>
    <v-navigation-drawer
      v-model="drawer"
      :color="theme === false ? 'teal lighten-1' : ''"
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
      :color="theme === false ? 'teal lighten-1' : ''"
      :collapse-on-scroll="drawer === false ? collapsed : !collapsed"
      :clipped-left="true"
      :collapse="drawer === false ? collapsed : !collapsed"
      fixed
      app
      dark
    >
      <v-app-bar-nav-icon @click="drawer = !drawer" />
      <v-spacer />
      <v-checkbox
        v-model="theme"
        hide-details
        color="white"
        @change="changeTheme"
      ></v-checkbox>
    </v-app-bar>
    <!-- ------------------------- -->
    <v-content>
      <v-container>
        <nuxt />
      </v-container>
    </v-content>
    <!-- ------------------------- -->
    <v-footer fixed app>
      <span>&copy; AppName&trade; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      theme: false,
      collapsed: true,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: "mdi-apps",
          title: "Welcome",
          to: "/"
        },
        {
          icon: "mdi-chart-bubble",
          title: "Inspire",
          to: "/inspire"
        }
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: "Vuetify.js"
    }
  },
  methods: {
    changeTheme() {
      this.$vuetify.theme.dark = this.theme
    }
  }
}
</script>
