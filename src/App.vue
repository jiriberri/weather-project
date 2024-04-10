<template>
  <div id="app">
    <div class="search-bar">
      <input type="text" class="search" placeholder="Search">
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data () {
    return {
      api_key: '642f37328cb1fc0a2c281c1289fe2e51'
    } 
  }
}
</script>

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  body {
    font-family: 'roboto', sans-serif;
  }

  
</style>
