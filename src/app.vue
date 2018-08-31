<template>
  <div id="app">
    <StencilCover v-if="cover === 'stencil'" title="vue min" :theme="theme">
      <template slot="subTitle">
        <h4>a minimal ui library by colin mcneil</h4>
      </template>

      <template slot="top">
        <h4 @click="next">Next Cover</h4>
      </template>

      <template slot="right">
        <h4 @click="tiles">View Tiles</h4>
      </template>

      <template slot="bottom">
        <h4 @click="pickerShown=true">Select Color</h4>
      </template>

      <template slot="left">
        <h4><a href="github.com/colinmcneil">View repo</a></h4>
      </template>
    </StencilCover>

    <PeekCover v-if="cover === 'peek'" title="vue min" :theme="theme">
      <template slot="subHeader">
        <h4>a minimal ui library by colin mcneil</h4>
      </template>
      <template slot="topLeft">
        <h4 @click="next">Next Cover</h4>
      </template>
      <template slot="topRight">
        <h4 @click="pickerShown=true">Select Color</h4>
      </template>
    </PeekCover>
    <RepelCover v-if="cover === 'repel'" title="vue min" :theme="theme">
      <template slot="subHeader">
        <h4>a minimal ui library by colin mcneil</h4>
      </template>
      <template slot="left">
        <h4 @click="next">Next Cover</h4>
      </template>
      <template slot="right">
        <h4 @click="pickerShown=true">Select Color</h4>
      </template>
    </RepelCover>
    <ColorPicker v-show="pickerShown" :click="()=>{pickerShown=false}" :change="setPrimary" :theme="theme"/>
    <br/>
    <ColorPicker v-show="pickerShown" :click="()=>{pickerShown=false}" :change="setSecondary" :theme="theme"/>
  </div>
</template>

<script>
import StencilCover from './components/VMinCover-Stencil'
import PeekCover from './components/VMinCover-Peek'
import RepelCover from './components/VMinCover-Repel'

import ColorPicker from './components/VMin-ColorPick.vue'

const covers = ['stencil', 'peek', 'repel']
export default {
  name: 'app',
  components: {
    StencilCover,
    PeekCover,
    RepelCover,
    ColorPicker
  },
  data(){
    return {
      theme: {
        primaryColor: 'rgb(74, 204, 206)',
        secondaryColor: '#FFF'
      },
      cover: 'stencil',
      pickerShown: false
    }
  },
  methods: {
    next() {
      let current = covers.indexOf(this.cover)
      if(current == covers.length - 1) return this.cover = covers[0]
      return this.cover = covers[current + 1]
    },
    tiles(){

    },
    setPrimary(h, s, v){
      this.theme.primaryColor = `hsl(${h}, ${s}%, ${v}%)`
    },
    setSecondary(h, s, v){
      this.theme.secondaryColor = `hsl(${h}, ${s}%, ${v}%)`
    },
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
a {
  color: inherit;
  text-decoration: none;
}
</style>
