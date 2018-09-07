<template>
  <div class="container" @mousemove="move" @click="move" ref="container"
    v-bind:style="{backgroundColor: theme.secondaryColor, color: theme.primaryColor}">
    <div class="bars topBars">
      <div class="bar topBar" v-for="bar in bars" :key="bar"
      :style="{ backgroundColor:theme.primaryColor, maxHeight: getHeight(bar)}">

      </div>
    </div>

    <div class="bars bottomBars">
      <div class="bar bottomBar" v-for="bar in bars" :key="bar"
      :style="{ backgroundColor:theme.primaryColor, maxHeight: getHeight(bar)}">

      </div>
    </div>
    
    <div class="cover center" >
      <h1 class="title">{{title}}</h1>
      
      <slot name="subTitle" class="subTitle"></slot>
    </div>
    <div class="cover left" >
      <slot name="left"></slot>
    </div>
    <div class="cover right" >
      <slot name="right"></slot>
    </div>
    
    
  </div>
</template>
<script>
export default {
  name: "Cover",
  props:{
    "title": {required: false, type: String},
    "theme": {required: false, type: Object, default: () =>({
         primaryColor: '#FFF', 
         secondaryColor: '#000'
      }),
    },
    "bars":{required: false, type: Number, default: 15}
  },
  data(){
    return {x:0, selectedBar: 0 }
  },
  methods:{
    move(event){
      let x = event.clientX
      this.x = x
    },
    getHeight(bar){
      return( 50 + Math.abs(bar-this.selectedBar) * 6) +'%'
    }
  },
  watch:{
    x(){
      if(!this.$refs.container) return '50%'
      let width = this.$refs.container.clientWidth
      let barWidth = width/this.bars
      this.selectedBar = Math.ceil(this.x/barWidth)
      
    }
  }
}
</script>
<style scoped>
@import url('https://fonts.googleapis.com/css?family=Raleway');
.bars {
  display: flex;
}
.topBars {
  top: 0;
  width: 100%;
  height: 50%;
  position: fixed;
}
.bottomBars {
  bottom: 0;
  width: 100%;
  height: 50%;
  position: fixed;
  align-items: flex-end;
}
.bar {
  max-height: 100%;
  height: 100%;
  width: 100%;
  transition: max-height ease 0.1s;
}
.bottomBar {
  bottom: 0;
}
.container {
  font-family: "Raleway";
  background-color: black;
  width:100%;
  height: 100%;
  position: fixed;
  top:0;
  left:0;
}
.cover {
  position: fixed;
  margin: 1em;
}
.center {
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
.title {
  font-size: 9em;
  margin: 0;
  
  font-variant: small-caps;
  line-height: 0.7em;
}
.subTitle {
  margin: 0;
  margin-top: 1em;
}
.right {
  top:50%;
  right: 0;
  font-size: 2em;
  cursor: pointer;
  transform: translateY(-50%);
}
.left {
  top: 50%;
  transform: translateY(-50%);
  left: 0;
  font-size: 2em;
  cursor: pointer;
}
@media (hover: none) { 
  .bar {
    opacity: 0.5;
  }
}
</style>
