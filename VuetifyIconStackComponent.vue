<template>
<div ref="ctnr" @click.prevent="clicked">
  <slot/>
</div>
  
</template>
<style scoped>

</style>
<script>
import {EventBus} from "@aphorica/vue-event-bus"

export default {
  name: 'vuetify-icon-stack',
  props: {
            initialState: {
              type: [String,Number],
              required: true
            }
          },
  data: function() {return{
    currentState: this.initialState
  }},
  mounted() {
    this.stateSet = {}

    for (let icon of this.$refs.ctnr.children)
      this.stateSet[icon.dataset.state] = icon

    this.setIconVisibility()

    EventBus.$on('set-vuetify-icon-stack-state', this.setState)
  },
  beforeDestroy() {
    EventBus.$off('set-vuetify-icon-stack-state', this.setState)
  },
  methods: {
    clicked() {
      console.log('in Clicked...')
      this.$emit('clicked', this.currentState)
    },
    setState(newState) {
      if (newState in this.stateSet) {
        this.currentState = newState
        this.setIconVisibility()
      }
    },
    setIconVisibility() {
      for (let stateItemKey of Object.keys(this.stateSet))
        this.stateSet[stateItemKey].style.display = 
          stateItemKey === this.currentState?
            'block' : 'none'
    }
  }
}
</script>
