<template>
  <div id="app">
    <indexSelect />
  </div>
</template>

<script>
import indexSelect from './indexSelect.vue'
export default {
  name: 'App',
  components: {
    indexSelect
  }
}
</script>

<style>
#app{
  height: 3000px;
}
</style>
