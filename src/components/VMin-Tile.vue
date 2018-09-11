<template>
  <div class="container" v-bind:style="{borderColor: theme.secondaryColor, color: secondary, backgroundColor: primary}">
    <div class="titleBar" v-show="title" v-bind:style="{backgroundColor: secondary, color: primary}">
      <h2 class="title">{{title}}</h2>
      </div>
    <slot class="content"/>
  </div>
</template>
<script>
export default {
  props: {
    "theme": {
        required: false, type: Object, default: () =>({
          primaryColor: '#FFF', 
          secondaryColor: '#000'
      })
    },
    "title":{
      type: String
    }
  },
  computed:{
    primary(){
      if(this.$store && this.$store.state.theme){
        return this.hovered 
        ? this.$store.state.theme.secondaryColor 
        : this.$store.state.theme.primaryColor
      }
      return this.hovered ? this.theme.secondaryColor : this.theme.primaryColor
    },
    secondary(){
      if(this.$store && this.$store.state.theme){
        return this.hovered 
        ? this.$store.state.theme.primaryColor 
        : this.$store.state.theme.secondaryColor
      }
      return this.hovered ? this.theme.primaryColor : this.theme.secondaryColor
    },
  }
  
}
</script>
<style scoped>
  .container {
    margin: 1em;
    border: solid black 1px;
  }
  .titleBar {

  }
  .title {
    margin: 0;
    text-transform: uppercase;
    font-weight: lighter;
  }

</style>
