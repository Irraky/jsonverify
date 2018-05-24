<template>
  <div id="wrapper">
    <div class="info">
      JSON verify
    </div>
    <textarea v-model="myjson" type="text" placeholder="Place your JSON here">

    </textarea>
    <br>
    <br>
    <select v-model="selected">
      <option disabled value="">Spaces for a tab</option>
      <option>2</option>
      <option>3</option>
      <option>4</option>
      <option>5</option>
    </select>
    <button v-on:click="check" v-if="selected">Test my JSON</button>
    <div>{{ errortext }}</div>
  </div>
</template>

<script>

// var JSON = require('json-bourne')

let data = {
  myjson: '',
  errortext: '',
  selected: 0
}
export default ({
  name: 'landingpage',
  data: function () {
    return data
  },
  methods: {
    check: function () {
      try {
        JSON.parse(this.myjson)
      } catch (err) {
        if (err) {
          this.errortext = '' + err
          return
        }
      }
      this.errortext = ''
      this.myjson = JSON.stringify(JSON.parse(this.myjson), null, parseInt(this.selected, 10))
    }
  }
})
</script>

<style>
  @import url('https://fonts.googleapis.com/css?family=Source+Sans+Pro');

  * {
    background-color: rgb(255, 255, 255);
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  .info {
    color : #21abca;
    text-align: center;
    font-size: 2em;
    padding-bottom: 15%;
  }

  body {
    font-family: 'Source Sans Pro', sans-serif; 
  }

  textarea {
    background-color: rgb(212, 215, 232);
    padding:3px;
    border:1px solid rgba(0, 102, 255, 0.514);
    border-block-start-color: blue;
    border-block-end-color: red;
    border-color: green;
    -ms-scrollbar-base-color: black;
    scrollbar-base-color: black;
    border-inline-start-color: black;
    caret-color: green;
    border-radius:5px;
    width:500px;
    height:600px;
    -ms-scroll-limit-x-min: 0px;
    word-wrap: physical;
    scroll-behavior: initial;
    
  }

  #wrapper {
    height: 100vh;
    padding: 60px 80px;
    width: 100vw;
  }
</style>