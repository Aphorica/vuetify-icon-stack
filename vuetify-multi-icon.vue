<template>
<div>
  <v-icon v-for="iconDef in iconDefs" :key="iconDef.state"
    :vshow="currentState === iconDef.state"
     @click="()=>clicked(iconDef.state)">
     {{iconDef.name}}
  </v-icon>
</div>
  
</template>
<style scoped>

</style>
<script>
import {EventBus} from "@aphorica/vue-event-bus"

export default {
  name: 'vuetify-icon-stack',
  props: [{
            name: "iconDefs",
            type: Object,
            required: true
          },
          {
            name: "initialState",
            type: [String,Number],
            required: true
          },
          {
            name: "size",
            type: String,
            required: false
          }
         ],
  data: function() {return{
    currentState: '',
    stateSet: null
  }},
  created() {
    this.stateSet = new Set()
    for (iconDef of iconDefs)
      this.stateSet.add(iconDef.state)

    EventBus.$on('set-vuetify-icon-stack-state', setState)
  },
  beforeDestroy() {
    EventBus.$off('set-vuetify-icon-stack-state', setState)
  },
  methods: {
    clicked(state) {
      EventBus.$emit('vuetify-icon-stack-state', state)
    },
    setState(newState) {
      if (this.stateSet.has(newState))
        this.currentState = newState
    }
  }
}
</script>
