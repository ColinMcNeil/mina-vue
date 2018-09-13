<template>
  <div class="container buttonGroup"
    v-bind:style="{borderColor: theme.secondaryColor, 
    color: secondary, backgroundColor: primary}">
    <slot :theme="theme"/>
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
.container.buttonGroup {
  display: flex;
  border: solid black 1px;
  border-radius: 2px;
}


.container.buttonGroup *{
  border: none;
  border-radius: 0px;
  border-right: solid black 0.5px;
  padding: 0.4em;
}
</style>
