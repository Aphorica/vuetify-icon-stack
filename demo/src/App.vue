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
      <v-btn icon @click="()=>setStackedIconState('add')">
        <v-icon large>mdi-plus-circle</v-icon>
      </v-btn>
      <v-btn icon @click="()=>setStackedIconState('abort')">
        <v-icon large>mdi-close-circle</v-icon>
      </v-btn>
      <v-btn icon @click="()=>setStackedIconState('commit')">
        <v-icon large>mdi-check-circle</v-icon>
      </v-btn>    </v-app-bar>

    <v-content>
      <v-row class="main" justify="center" align="center">
        <vuetify-icon-stack :initialState="currentState"
          @clicked="onStackIconClicked">
          <v-icon data-state="add" color="primary" x-large>mdi-plus-circle</v-icon>
          <v-icon data-state="commit" color="primary" x-large>mdi-check-circle</v-icon>
          <v-icon data-state="abort" color="black" x-large>mdi-close-circle</v-icon>
        </vuetify-icon-stack>
      </v-row>
    </v-content>
    <v-footer absolute dark>
      {{footerText}}
    </v-footer>
  </v-app>
</template>

<style>
  .main { height:100%; }
  html { overflow-y:hidden!important; }
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
    ],
    currentState: 'add',
    footerText: ''
  }},
  created() {
    this.defaultFooterText = '(Click icon stack...)'
    this.footerText = this.defaultFooterText
  },
  methods: {
    setStackedIconState(state) {
      EventBus.$emit('set-vuetify-icon-stack-state', state)
      this.footerText = this.defaultFooterText
    },
    onStackIconClicked(state) {
      this.currentState = state
      this.footerText = "Stacked icon clicked: " + state
    }
  }
};
</script>
