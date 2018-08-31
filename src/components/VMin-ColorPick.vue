<template>
  <div class="container">
    <div class="closeBar" @click="click" @mouseover="hovered='close'" 
    @mouseleave="hovered=''"
    :style="{backgroundColor: getCSS('close', 'backgroundColor'), 
    color: getCSS('close', 'color')}">
      {{hovered==='close'? 'Close':'X'}}
    </div>
    <div class="content">
      <div class="preview" 
      :style="{backgroundColor: `hsl(${h}, ${s}%, ${v}%)`, color: v>50 ? 'black' : 'white'}">
      HSV: {{h}}, {{s}}%, {{v}}%
      
      </div>
      <div class="picker hue">
        <div v-for="hue in 360" :key="hue" class="bar"
        :style="{backgroundColor: `hsl(${hue}, 100%, 50%)`}"
        @click="h=hue">
        </div>
      </div>
      <div class="picker saturation">
        <div v-for="saturation in 100" :key="saturation" class="bar cent"
        :style="{backgroundColor: `hsl(${h}, ${saturation}%, 50%)`}"
        @click="s=saturation">
        </div>
      </div>
      <div class="picker value">
        <div v-for="value in 100" :key="value" class="bar cent"
        :style="{backgroundColor: `hsl(${h}, ${s}%, ${value}%)`}"
        @click="v=value">
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props:{
    click: {type: Function, required: false, default: ()=>{}},
    change: {type: Function, required: false, default: ()=>{}},
    "theme": {
        required: false, type: Object, default: () =>({
          primaryColor: '#FFF', 
          secondaryColor: '#000'
      })
    }
  },
  data:() =>({
    h:0,
    s: 50,
    v: 50,
    hovered: ''
  }),
  watch:{
    h(){this.change(this.h,this.s,this.v)},
    s(){this.change(this.h,this.s,this.v)},
    v(){this.change(this.h,this.s,this.v)}
  },
  methods:{
    getCSS(name, tag){
      switch(tag){
        case 'backgroundColor':
          return this.hovered===name ? this.theme.secondaryColor:this.theme.primaryColor
          break
        case 'color':
          return this.hovered===name ? this.theme.primaryColor:this.theme.secondaryColor
          break
      }
      
    }
  }
}
</script>
<style scoped>
@import url('https://fonts.googleapis.com/css?family=Raleway');
.container {
  background-color: rgba(0,0,0,0.6);
  color: white;
  width: 300px;
  position: relative;
  display: flex;
  flex-direction: column;
  font-family: 'Raleway';
  border-radius: 2px;
}
.closeBar {
  height: 1.1em;
  width: 100%;
  background-color: white; 
  cursor: pointer;
  transition: all ease 0.3s;
  filter: brightness(80%);
}
.closeBar:hover {
  height: 1.5em;
  filter: brightness(100%);
}
.content {
  padding: 1em;
}
.preview {
  width: 90%;
  height: 1.5em;
  font-size: 1.2em;
}
.picker {
  display: flex;
  width: 90%;
  height: 1.5em;
  margin-top: 1em;
  border-radius: 2px;
}
.bar {
  width: .29%;
}
.bar.cent {
  width: 1%;
}
.bar:hover {
  flex: 2 2 1em;
  border-right: solid black 1px;
  border-left: solid black 1px;
}
.hue{
  margin-left: 10%;
}
.value {
  margin-left: 10%;
}
</style>


