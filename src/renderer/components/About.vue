<template>
  <div id="logodiv">
    About
    <router-link id="button" to="/Home">Go to Home Page</router-link>
  </div>
</template>

<script>
  export default {
    name: 'about'
  }
</script>

<style>


  * {
    background-color: rgb(255, 255, 255);
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  #logodiv {
    color: #21abca;
    text-align: center;
    font-size: 2em;
  }

</style>