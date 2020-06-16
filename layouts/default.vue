<template>
  <v-app>
    <app-navbar />
    <!-- ------------------------- -->
    <v-content>
      <nuxt />
    </v-content>
    <!-- ------------------------- -->
    <v-footer fixed app>
      <span>&copy; Talha Karasu&trade; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
import AppNavbar from "@/components/AppHeader"
export default {
  components: {
    AppNavbar
  },
  data() {
    return {
      theme: false
    }
  }
}
</script>
