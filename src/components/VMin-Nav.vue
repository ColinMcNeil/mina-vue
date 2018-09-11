<template>
  <div class="container nav">
    <div class="nav">
      <slot :theme="theme"/>
    </div>
    
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
.container.nav {
  position: fixed;
  width: 100%;
  top:0;
  left:0;
  margin: 2em;
}
.nav{
  display: flex;
}
.nav * {
  margin: 0.2em;
}
</style>
