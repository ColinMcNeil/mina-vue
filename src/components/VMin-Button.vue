<template>
  <div class="container" @click="click" v-on:mouseover="hovered=true" 
  @mouseleave="hovered=false"
  v-bind:style="{borderColor: theme.secondaryColor, color: secondary, backgroundColor: primary}">
    <slot :theme="theme"/>
  </div>
</template>
<script>
export default {
  props:{
    "link":{required: false},
    "click":{required: false},
    "type":{required: false, type: String},
    "theme": {
        required: false, type: Object, default: () =>({
          primaryColor: '#FFF', 
          secondaryColor: '#000'
      }),
    },
  },
  data: () =>({hovered: false}),
  computed: {
    primary(){
      let primaryColor = this.theme.primaryColor;
      let secondaryColor = this.theme.secondaryColor;
      if(this.$store && this.$store.state.theme) {
        primaryColor = this.$store.state.theme.primaryColor
        secondaryColor = this.$store.state.theme.secondaryColor
      }
      if(this.type === 'error') {
        primaryColor = 'rgb(200, 70, 70)'
        secondaryColor = 'rgb(250, 70, 70)'
      }
      if(this.type === 'success') {
        primaryColor = 'rgb(49, 188, 109)'
        secondaryColor = 'rgb(49, 210, 100)'
      }
      if(this.type === 'disabled') {
        primaryColor = 'rgb(120, 120, 120)'
        secondaryColor = 'rgb(150, 150, 150)'
      }
      if(this.hovered) return secondaryColor
      return primaryColor
    },
    secondary(){
      let primaryColor = this.theme.primaryColor;
      let secondaryColor = this.theme.secondaryColor;
      if(this.$store && this.$store.state.theme) { 
        primaryColor = this.$store.state.theme.primaryColor
        secondaryColor = this.$store.state.theme.secondaryColor
      }
      if(this.type === 'error') {
        primaryColor = secondaryColor
        secondaryColor = 'black'
      }
      if(this.type === 'success') {
        primaryColor = secondaryColor
        secondaryColor = 'black'
      }
      if(this.type === 'disabled'){
        secondaryColor = 'black'
      }
      if(this.hovered) return primaryColor
      return secondaryColor
    },
    dynamic(){
      console.log(typeof this.link)
      switch(typeof this.link){
        case 'string':
          break
        default:
          break
      }
    }
  }
}
</script>
<style scoped>
  .container {
    border: solid black 1px;
    border-radius: 2px;
    padding: 0.5em 1em 0.5em 1em;
    transition: all ease 0.2s;
    cursor: default;
    display: flex;
    justify-content: center;
    align-items: center;
    text-transform: lowercase;
    font-variant: small-caps;
  }
</style>
