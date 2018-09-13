<template>
  <div class="container nav" ref="nav">
    <div class="background" :style="{backgroundColor: primary}">
    </div>
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
  mounted(){
    window.document.body.onscroll = function() {
        console.log(123);
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
    }
  }
}
</script>
<style scoped>
.container.nav {
  width: 100%;
  top: 0;
  left: 0;
  padding: 1em;
  box-shadow: 5px 0px 0px 0px rgba(0, 0, 0, 0.8);
  box-sizing: border-box;
  position: sticky;
  z-index: 100;
  display: flex;
  justify-content: center;
}

.nav{
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  position: relative;
}
.nav * {
  margin: 0.2em;
}
.background {
  width: 100%;
  top: 0;
  margin: 0;
  left: 0;
  height: 50%;
  box-shadow: 5px 0px 0px 0px rgba(0, 0, 0, 0.8);
  box-sizing: border-box;
  position: absolute;
}
@media screen and (max-width: 400px){
  .background {
    height: 80%;
  }
}
</style>
