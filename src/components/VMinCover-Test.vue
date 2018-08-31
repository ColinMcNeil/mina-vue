<template>
  <div class="container" 
    v-bind:style="{backgroundColor: theme.primaryColor, color: theme.secondaryColor}">
    <div class="cover" v-bind:style= "{width: maxWidth}" >
      <h1 class="title">{{title}}</h1>
      
      <slot name="subTitle" class="subTitle"></slot>
    </div>
    <div class="side horizontal top">
      <hr :style="{width:randomWidths[0]}"/>
      <slot name="top"></slot>
      <hr :style="{width:randomWidths[0]}"/>
    </div>
    <div class="side vertical right">
      <hr :style="{width:randomWidths[1]}"/>
      <slot name="right"></slot>
      <hr :style="{width:randomWidths[1]}"/>
    </div>
    <div class="side horizontal bottom">
      <hr :style="{width:randomWidths[2]}"/>
      <slot name="bottom"></slot>
      <hr :style="{width:randomWidths[2]}"/>
    </div>
    <div class="side vertical left">
      <hr :style="{width:randomWidths[3]}"/>
      <slot name="left"></slot>
      <hr :style="{width:randomWidths[3]}"/>
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
      })
    }
  },
  data(){
    let randomWidths= []
    for(let i =0; i<10;i++){
      randomWidths.push(`${Math.random()*3+2}em`)
    }
    return {randomWidths: randomWidths}
  },
  computed: {
    maxWidth(){
      return `${this.title.length*3}em`
    },
    randomWidth(){
      return `${Math.random()*5}em`
    }
  }
}
</script>
<style scoped>
@import url('https://fonts.googleapis.com/css?family=Raleway');
.container {
  
}
.container {
  font-family: "Raleway";
  background-color: black;
  width:100%;
  height: 100%;
  position: fixed;
  top:0;
  left:0;
  color: white;
}
.cover {
  top: 10%;
  left: 10%;
  position: fixed;
}
hr {
  margin:1em;
  padding: 0;
  /* border: none; */
  color: white;
  transition: all 0.3s ease;
}
.title {
  word-break: break-all;
  font-size: 9em;
  margin: 0;
  font-variant: small-caps;
  line-height: 0.7em;
}
.subTitle {
  margin: 0;
  margin-top: 1em;
}
.side {
  position: fixed;
  font-size: 2em;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 50%;
  
  height: 1em;
  transition: ease all 0.3s;
}
.side:hover {
  cursor: pointer;
}
.side:hover hr {
  width: 5em;
  margin:1.2em 0.3em 1.2em 0.3em;
  color: white;
}
.horizontal {
  width: 100%;
}
.vertical {
  width: 20em;
  top:0;
  font-size: 1.5em;
}
.top {
  top:0.5em;
}
.right {
  transform: rotate(90deg) translate(70%, 5%);
  transform-origin: right;
  right: 1em;
  top: 50%;
}
.bottom {
  bottom: 0.5em;
}
.left {
  transform: rotate(270deg) translate(-30%, 60%);
  transform-origin: left;
  top: 40%;
}


</style>


