<template>
  <div class="container" @mousemove="move" @click="move" ref="container"
    v-bind:style="{backgroundColor: primary, color: primary, 
    textShadow: `-1px 0 ${secondary}, 0 0.5px ${secondary}, 0.5px 0 ${secondary}, 0 -0.5px ${secondary}`}">
    
    <div class="cusror" :style="{left: x, top: y, maxHeight: maxHeight , backgroundColor:secondary}"></div>
    
    <div class="cover center" >
      <h1 class="title">{{title}}</h1>
      <slot name="subTitle" class="subTitle"></slot>
    </div>

    <div class="cover topLeft" >
      <slot name="topLeft"></slot>
    </div>

    <div class="cover topRight" >
      <slot name="topRight"></slot>
    </div>
    
  </div>
</template>


<script>
export default {
  name:"VMin-Cover-Peek",
  props:{
    "title": {required: false, type: String},
    "theme": {required: false, type: Object, default: () =>({
         primaryColor: '#FFF', 
         secondaryColor: '#000'
      })
    }
  },
  data(){
    return {x:'0px', y:'0px', maxHeight: '100%'}
  },
  methods:{
    move(event){
      let x = event.clientX
      let width = this.$refs.container.clientWidth
      if(x > width * .75) {
        this.maxHeight = '50%'
        this.y = '50%'
      }
      else if (x < width * .25){
        this.maxHeight = '50%'
        this.y = '0%'
      }
      else {
        this.maxHeight = '100%'
        this.y = '0%'
      }
      
      this.x = x+'px'
      
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
@import url('https://fonts.googleapis.com/css?family=Raleway');
.cusror {
  width: 30%;
  height: 100%;
  position: fixed;
  top: 0;
  bottom:0;
  background-color: black;
  transform: translateX(-50%);
  transition: max-height ease 0.2s , top ease 0.2s;
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

.topLeft {
  top:0;
  left: 0;
  font-size: 2em;
  cursor: pointer;
}

.topRight {
  bottom:0;
  right: 0;
  font-size: 2em;
  cursor: pointer;
}

@media (hover: none) { 
  .cusror {
    width: 50%;
  }
}

@media not all and (hover: hover){
  .cover {
    text-shadow: none!important;
  }
}
</style>
