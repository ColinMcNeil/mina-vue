<template>
  <div id="app">
    <stencil-cover v-if="cover === 'stencil'" :title="title" :theme="theme">
      <template slot="subTitle">
        <h4>a minimal ui library by colin mcneil</h4>
      </template>

      <template slot="top">
        <h4 @click="next">Next Cover</h4>
      </template>

      <template slot="right">
        <h4 @click="tileShown = true">View Tiles</h4>
      </template>

      <template slot="bottom">
        <h4 @click="pickerShown=true">Select Color</h4>
      </template>

      <template slot="left">
        <h4><a href="github.com/colinmcneil">View repo</a></h4>
      </template>
    </stencil-cover>

    <peek-cover v-if="cover === 'peek'" :title="title" :theme="theme">
      <template slot="subHeader">
        <h4>a minimal ui library by colin mcneil</h4>
      </template>
      <template slot="topLeft">
        <h4 @click="next">Next Cover</h4>
      </template>
      <template slot="topRight">
        <h4 @click="pickerShown=true">Select Color</h4>
      </template>
    </peek-cover>
    <repel-cover v-if="cover === 'repel'" :title="title" :theme="theme">
      <template slot="subHeader">
        <h4>a minimal ui library by colin mcneil</h4>
      </template>
      <template slot="left">
        <h4 @click="next">Next Cover</h4>
      </template>
      <template slot="right">
        <h4 @click="pickerShown=true">Select Color</h4>
      </template>
    </repel-cover>
    <dash :theme="theme" v-if="tileShown">
      <nav >
        <v-min-button :theme="theme" :click="click">Button 1</v-min-button>
        <v-min-button :theme="theme" :click="click">Button 2</v-min-button>
        <v-min-button :theme="theme" :click="click">Button 3</v-min-button>
        <v-min-button :theme="theme" :click="click">Close</v-min-button>

        <v-min-button-group :theme="theme">
          <v-min-button :theme="theme" :click="click">Regular</v-min-button>
          <v-min-button :theme="theme" :type= "disabled ? 'disabled':''" :click="()=>disabled=!disabled">Disabled</v-min-button>
          <v-min-button :theme="theme" type="success" :click="click">Success</v-min-button>
          <v-min-button :theme="theme" type="error" :click="click">Error</v-min-button>
        </v-min-button-group>

      </nav>
      <tile-grid :theme="theme">
        <tile :theme="theme" title="Card1">
          Card 1 content
        </tile>
        <tile :theme="theme" title="Card2">
          Card 2 content
        </tile>
      </tile-grid>
    </dash>
    
    <ColorPicker v-show="pickerShown" :click="()=>{pickerShown=false}" :change="setPrimary" :theme="theme"/>
    <br/>
    <ColorPicker v-show="pickerShown" :click="()=>{pickerShown=false}" :change="setSecondary" :theme="theme"/>
  </div>
</template>

<script>
import StencilCover from './components/VMinCover-Stencil'
import PeekCover from './components/VMinCover-Peek'
import RepelCover from './components/VMinCover-Repel'

import TileGrid from './components/VMin-Tile-Grid'
import Dash from './components/VMin-Dash'
import Tile from './components/VMin-Tile'
import Nav from './components/VMin-Nav'

import ColorPicker from './components/VMin-ColorPick'
import VMinButton from './components/VMin-Button'
import VMinButtonGroup from './components/VMin-Button-Group'

const covers = ['stencil', 'peek', 'repel']
export default {
  name: 'app',
  components: {
    StencilCover,
    PeekCover,
    RepelCover,
    ColorPicker,
    Tile,
    TileGrid,
    Dash,
    Nav,
    VMinButton,
    VMinButtonGroup
  },
  data(){
    return {
      theme: {
        primaryColor: 'rgb(74, 204, 206)',
        secondaryColor: '#FFF'
      },
      cover: 'stencil',
      pickerShown: false,
      tileShown: false,
      title: 'vue min',
      disabled: false,
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
    click(){
      console.log('click')
    }
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
}
a {
  color: inherit;
  text-decoration: none;
}
</style>
