<template>
  <div class="container breadcrumb" @click="click || null" v-on:mouseover="hovered=true" 
  @mouseleave="hovered=false"
  v-bind:style="{color: secondary, backgroundColor: primary, borderColor: secondary}">
    <slot :theme="theme"/>
    
    <VMinButton :theme="theme" class="close" :click="close" v-show="close">x</VMinButton>
  </div>
</template>
<script>
import VMinButton from './VMin-Button'
export default {
  name:"VMin-Breadcrumb",
  props:{
    "click":{required: false,},
    "type":{required: false, type: String},
    "close":{required: false, type: Function},
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
        secondaryColor = 'rgb(120, 120, 120)'
        primaryColor = 'rgb(150, 150, 150)'
      }
      if(this.hovered) return primaryColor
      return secondaryColor
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
        secondaryColor = 'white'
        primaryColor = 'white'
      }
      if(this.hovered) return secondaryColor
      return primaryColor
    },
    dynamic(){
      console.log(typeof this.link)
      switch(typeof this.link){
        case 'string':
          break
        default:
          break
      }
    },
  },
  components:{
      VMinButton
  }
}
</script>
<style scoped>
  .container.breadcrumb {
    border-radius: 1px;
    border: solid 1px;
    padding: 0.1em 0.1em 0.1em 0.1em;
    transition: all ease 0.2s;
    cursor: default;
    margin:0.1em;
    display: inline-flex;
    justify-content: center;
    align-items: center;
    text-transform: lowercase;
    font-variant: small-caps;
  }
  .close {
    margin-left: 0.2em;
    background-color: rgba(0,0,0,0.2);
    padding: 0 0.2em 0 0.2em;
    border: none;
    border-radius: 1px;
  }
</style>
