<template>
  <div>
    <h1 id="logodiv">About</h1>
    <footer>
    <router-link id="button" to="/Home">Go to Home Page</router-link>
    </footer>
  </div>
</template>

<script>
  export default {
    name: 'about'
  }
</script>

<style>

  #logodiv {
    color: #21abca;
    text-align: center;
    font-size: 2em;
  }

</style>