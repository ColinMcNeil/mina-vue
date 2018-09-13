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
        <h4><a href="https://www.github.com/colinmcneil/mina-vue">View repo</a></h4>
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
      <v-min-nav :theme="theme">
        <v-min-button :theme="theme" :click="click">Button 1</v-min-button>
        <v-min-button :theme="theme" :click="click">Button 2</v-min-button>
        <v-min-button :theme="theme" :click="click">Button 3</v-min-button>
        <v-min-button :theme="theme" type="success" :click="()=>tileShown=false"><h3>Home</h3></v-min-button>

        <v-min-button-group :theme="theme">
          <v-min-button :theme="theme" :click="click">Regular</v-min-button>
          <v-min-button :theme="theme" :type= "disabled ? 'disabled':''" :click="()=>disabled=!disabled">Disabled</v-min-button>
          <v-min-button :theme="theme" type="success" :click="click">Success</v-min-button>
          <v-min-button :theme="theme" type="error" :click="click">Error</v-min-button>
        </v-min-button-group>

      </v-min-nav>
      <tile-grid :theme="theme">
        <tile key="1" :theme="theme" title="Primary Color">
          <ColorPicker :change="setPrimary" :theme="theme"/>
        </tile>
        <tile key="2" :theme="theme" title="Breadcrumbs">
          <div class="flex">
            <v-min-breadcrumb :theme="theme" >Delicious</v-min-breadcrumb>
            <transition name="fade">
            <v-min-breadcrumb 
            :theme="theme" :type= "disabled ? 'disabled':''" 
            :close="()=>disabled=!disabled" v-show="disabled">
              Nutritious
            </v-min-breadcrumb>
            </transition>
            <v-min-breadcrumb :theme="theme" >Epic</v-min-breadcrumb>
            <v-min-breadcrumb :theme="theme" >Cool.</v-min-breadcrumb>
            <v-min-breadcrumb :theme="theme" > Wow</v-min-breadcrumb>
          </div>
        </tile>
        <tile key="3" :theme="theme" title="Alerts">
          <div class="padded">
            <v-min-button :theme="theme" :click="()=>alerts.push(`Alert${alertCount+=1}`)">Alert!</v-min-button>
          </div>
        </tile>
        <tile key="4" :theme="theme" title="Card4">
          <h3>Card 4 content</h3>
        </tile>
        <tile key="5" :theme="theme" title="Secondary Color">
          <ColorPicker :change="setSecondary" :theme="theme"/>
        </tile>
        <tile key="6" v-show="disabled" :theme="theme" title="Card6">
          <h3>Card 6 content</h3>
        </tile>
        <tile key="7" :theme="theme" title="Card7">
          <h3>Card 7 content</h3>
        </tile>
        <tile key="8" :theme="theme" title="Card8">
          <h3>Card 8 content</h3>
        </tile>
        <tile key="9" :theme="theme" title="Card9">
          <h3>Card 9 content</h3>
        </tile>
      </tile-grid>
      <vmin-alerts :theme="theme" :alerts="alerts"/>
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
import VMinNav from './components/VMin-Nav'

import ColorPicker from './components/VMin-ColorPick'
import VMinButton from './components/VMin-Button'
import VMinButtonGroup from './components/VMin-Button-Group'
import VMinBreadcrumb from './components/VMin-Breadcrumb'
import VminAlerts from './components/VMin-Alerts'

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
    VMinNav,
    VMinButton,
    VMinButtonGroup,
    VMinBreadcrumb,
    VminAlerts
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
      title: 'mina vue',
      disabled: true,
      alerts: [],
      alertCount: 0
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
h1, h2, h3, h4 {
  margin: 0.2em;
}
h3 {
  font-size: 1.3em;
}
.flex {
  display: flex;
  flex-wrap: wrap;
  max-width: 200px;
  padding: 0.5em;
}
.padded {
  padding: 1em;
}
.fade-enter-active, .fade-leave-active {
  transition: opacity .2s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>
