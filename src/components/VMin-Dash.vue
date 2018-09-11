<template>
  <div class="dash container" v-bind:style="{backgroundColor: primary, color: primary}">
    <slot :theme="theme" class="grid"/>
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
.dash.container {
  position: fixed;
  width: 100%;
  height: 100%;
  left:0;
  top: 0;
  display: flex;
  flex-direction: column;
  overflow-y: auto;
}
</style>
