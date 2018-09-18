<template>
  <div class="container tileGrid">
    <slot class="grid"/>
  </div>
</template>
<script>
export default {
  name:"VMin-Tile-Grid"
}
</script>

<style scoped>
.tileGrid {
  margin-top: 1em;
  padding: 1em;
  display: flex;
  flex-wrap: wrap;
  padding: 0 20%;
  justify-content: center;
}
.tileGrid .container.tile {
  margin-bottom: 3em;
  flex-basis: 25%;
}
</style>
