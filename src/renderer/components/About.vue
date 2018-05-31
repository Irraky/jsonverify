<template>
  <div>
    <h1 id="logodiv">About</h1>
    <h2>Why ?</h2>
    <p>
      I made this site to learn more things about JS and to have something to check and format my JSON quickly.
      <br>
      The tree structure is here to make everyone understand and modify the JSON easily.
    </p>
    <h2>Who</h2>
    <p>
      Irraky, from <a href="http://www.soixantecircuits.fr/">Soixante circuits</a>
    </p>
    <h2></h2>
    <p>
    </p>
    <footer>
      <router-link id="button" to="/Home">Go to Home Page</router-link>
      <hr />
	    <p style="font-family:monospace;text-align:right;" ><i>©Irraky</i></p>
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