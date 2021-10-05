<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
       <h4>Find Your Age</h4>
      </div>

      <v-spacer></v-spacer>

    </v-app-bar>

    <v-main>
      <AgeComponent/>
    </v-main>
  </v-app>
</template>

<script>
import AgeComponent from './components/AgeComponent';

export default {
  name: 'App',

  components: {
    AgeComponent,
  },

  data: () => ({
    //
  }),
};
</script>
