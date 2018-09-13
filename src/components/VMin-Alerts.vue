<template>
  <div class="container alerts" @click="click || null"
  v-bind:style="{color: secondary, borderColor: secondary}">
    <transition-group class="alertsInner" name="alertFade">
      <div class="alert" v-for="(alert,index) in alerts" :key="index" 
      :style="{backgroundColor: primary}" 
      @click="()=>{alerts.splice(index,1)}"
      @mouseover="hoveredI=index" @mouseleave="hoveredI = -1">
        {{hoveredI===index ? 'dismiss' : alert}}
      </div>
    </transition-group>
  </div>
</template>
<script>
import VMinButton from './VMin-Button'
export default {
  name:"VMin-Alert",
  props:{
    "alerts":{required: false, default: ()=>[]},
    "type":{required: false, type: String},
    "theme": {
        required: false, type: Object, default: () =>({
          primaryColor: '#FFF', 
          secondaryColor: '#000'
      }),
    },
  },
  data: () =>({hovered: false, hoveredI:-1}),
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
  .alertsInner {
    position: fixed;
    bottom: 1em;
    right: 1em;
    width: 30%;
    min-width: 10em;
    display: flex;
    flex-direction: column;
  }
  .close {
    margin-left: 0.2em;
    background-color: rgba(0,0,0,0.2);
    padding: 0 0.2em 0 0.2em;
    border: none;
    border-radius: 1px;
  }
  .alert {
    display: flex;
    width: 100%;
    margin: 0.5em 0;
    padding: 0.5em;
    box-sizing: border-box;
    justify-content: space-between;
    align-items: center;
    cursor: default;
  }
  .alert .container.button {
    border-radius: 0;
    padding: 0.4em;
    align-self: flex-end;
    height: 100%;
    width: 4em;
  }
  .alertFade-move {
    transition: transform 0.3s;
  }
  .alertFade-enter-active, .alertFade-leave-active {
    transition: all 0.3s;
    
  }
  .alertFade-enter, .alertFade-leave-to /* .list-leave-active below version 2.1.8 */ {
    opacity: 0;
    transform: translateY(10px);
  }
  .alertFade-leave-active {
    position: absolute;    
  }
</style>
