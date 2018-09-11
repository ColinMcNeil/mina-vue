<template>
  <div class="container tileGrid">
    <slot class="grid"/>
  </div>
</template>
<style scoped>
.container.tileGrid {
  margin-top: 1em;
  padding: 1em;
  display: flex;
  flex-wrap: wrap;
}
.grid {
  
}
</style>
