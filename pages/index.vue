<template>
  <v-container>
    <v-layout column justify-center align-center>
      <v-flex xs12 sm8 md6>
        <v-card>
          <v-card-title class="headline">
            WELCOME TO COVID-19 CASES APP
          </v-card-title>
          <v-card-text>
            You can go to the github repository of this project or continue to
            the app
          </v-card-text>
          <v-card-actions>
            <v-spacer />
            <v-btn
              color="primary"
              target="_blank"
              href="https://github.com/TalhaK15/covid-19"
            >
              Go to the Github Repository
            </v-btn>
            <v-btn color="primary" nuxt to="/covid">
              Continue to the App
            </v-btn>
            <v-spacer />
          </v-card-actions>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
export default {}
</script>
