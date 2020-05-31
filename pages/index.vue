<template>
  <v-container>
    <v-row justify="center" align="center">
      <v-col cols="12">
        <v-card>
          <v-card-title class="headline">
            <v-spacer />
            WELCOME TO COVID-19 CASES APP
            <v-spacer />
          </v-card-title>
          <v-card-text>
            You can go to the github repository of this project or continue to
            the app
          </v-card-text>
          <v-card-actions>
            <v-row justify="space-between">
              <v-col cols="12" sm="6">
                <v-btn
                  color="primary"
                  target="_blank"
                  href="https://github.com/TalhaK15/covid-19"
                >
                  Go to the Github Repo
                </v-btn>
              </v-col>
              <v-col
                cols="12"
                sm="6"
                :class="{ 'text-right': $vuetify.breakpoint.smAndUp }"
              >
                <v-btn color="primary" nuxt to="/covid">
                  Continue to the App
                </v-btn>
              </v-col>
            </v-row>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {}
</script>
