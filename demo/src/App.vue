<template>
  <v-app>
    <v-app-bar
      app
      dense
      color="primary"
      dark
    >
      <v-toolbar-title>Vuetify Icon Stack</v-toolbar-title>
      <v-spacer/>
      <v-btn icon @click="()=>onClick('add')">
        <v-icon large>mdi-plus-circle</v-icon>
      </v-btn>
      <v-btn icon @click="()=>onClick('abort')">
        <v-icon large>mdi-close-circle</v-icon>
      </v-btn>
      <v-btn icon @click="()=>onClick('commit')">
        <v-icon large>mdi-check-circle</v-icon>
      </v-btn>    </v-app-bar>

    <v-content>
      <v-row class="main" justify="center" align="center">
        <vuetify-icon-stack
          :iconDefs="iconDefs"
          initialState="add"
          size="50px" />
      </v-row>
    </v-content>
  </v-app>
</template>

<style>
  .main { height:100%; }
</style>

<script>
import VuetifyIconStackComponent from '../../VuetifyIconStackComponent'
import {EventBus} from '@aphorica/vue-event-bus'

export default {
  name: 'App',
  components: {"vuetify-icon-stack": VuetifyIconStackComponent},
  data: function() { return {
    iconDefs: [
      {
        name: 'mdi-plus-circle',
        state: 'add',
        color: 'primary'
      },
      {
        name: 'mdi-close-circle',
        state: 'abort',
        color: 'black'
      },
      {
        name: 'mdi-check-circle',
        state: 'commit',
        color: 'error'
      }
    ]
  }}
};
</script>
