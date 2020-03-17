<template>
<div>
  <v-icon v-for="iconDef in iconDefs" :key="iconDef.state"
    :vshow="currentState === iconDef.state"
    :style="setStyle(iconDef)"
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
  props: {
            iconDefs: {
              type: Array,
              required: true
            },
            initialState: {
              type: [String,Number],
              required: true
            },
            size: {
              type: String,
              required: false
            }
          },
  data: function() {return{
    currentState: '',
    stateSet: null
  }},
  mounted() {
    this.stateSet = new Set()
    for (let iconDef of this.iconDefs)
      this.stateSet.add(iconDef.state)

    EventBus.$on('set-vuetify-icon-stack-state', this.setState)
  },
  beforeDestroy() {
    EventBus.$off('set-vuetify-icon-stack-state', this.setState)
  },
  methods: {
    clicked(state) {
      EventBus.$emit('vuetify-icon-stack-state', state)
    },
    setState(newState) {
      if (this.stateSet.has(newState))
        this.currentState = newState
    },
    setStyle(iconDef) {
      if (iconDef.size) {
        return "height:50px;width:50px;"
        return "height:" + iconDef.size + '; width:' + iconDef.size
      }
    }
  }
}
</script>
