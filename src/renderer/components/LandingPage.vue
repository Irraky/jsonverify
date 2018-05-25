<template>
  <div id="wrapper">
    <div class="info">
      JSON verify
    </div>
    <div>
      <div class="numero" id="myscroll">
        0 <br>
        <span v-for="line in lines"> {{line}} <br> </span>
        <br>
      </div>
      <textarea v-model="myjson" type="text" placeholder="Place your JSON here"
      name="text" id="text" cols="30" v-on:keyup="keymonitor" v-on:keydown="keymonitor">
      </textarea>
    </div>
    <div class="input">
      <select v-model="selected">
        <option disabled value="">Spaces for a tab</option>
        <option>2</option>
        <option>3</option>
        <option>4</option>
        <option>5</option>
      </select>
      <button v-on:click="check" v-if="selected">Test my JSON</button>
      </div>
      <div v-if="error" class='error'>
        {{ errortext }}
      </div>
  </div>
</template>

<script type="text/javascript">
let data = {
  myjson: '',
  errortext: '',
  selected: 0,
  lines: 0,
  error: false
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
          this.error = true
          this.errortext = '' + err
          return
        }
      }
      this.error = false
      this.errortext = ''
      this.myjson = JSON.stringify(JSON.parse(this.myjson), null, parseInt(this.selected, 10))
    },
    keymonitor: function (event) {
      var text = document.getElementById('text')
      var scroll = document.getElementById('myscroll')
      if (text.value.match(/[\r\n]/g)) {
        this.lines = text.value.match(/[\r\n]/g).length
      } else {
        this.lines = 0
      }
      scroll.scrollTop = text.scrollTop + 2
      console.log(text.scrollTop)
    }
  }
})
</script>

<style>
  @import url('https://fonts.googleapis.com/css?family=Source+Sans+Pro');

  .info {
    color : #21abca;
    text-align: center;
    font-size: 2em;
  }

  body {
    font-family: 'Source Sans Pro', sans-serif;
    overflow: hidden;
  }

  textarea {
    background-color: rgb(212, 215, 232);
    padding:3px;
    border:1px solid rgba(0, 102, 255, 0.514);
    border-block-start-color: blue;
    width:500px;
    height:601px;
    word-wrap: physical;
    resize: none;
    overflow-y: hidden;
    display:inline-block;
    margin-left: -10px;
    font-size: 16px;
    line-height: 20px;
    font-family: 'Source Sans Pro', sans-serif;
  }

  textarea:focus {
    caret-color: #21abfa;
    outline: none;
    overflow-y: visible;
  }

  #wrapper {
    height: 100vh;
    padding: 60px 80px;
    width: 100vw;
  }


  .numero {
    font-family: 'Source Sans Pro', sans-serif;
    padding-top: 4px;
    background-color: rgb(195, 198, 211);
    color: rgb(99, 51, 187);
    width:45px;
    height: 605px;
    float: left;
    padding-left: 25px;
    font-size: 16px;
    line-height: 20px;
    overflow: hidden;
    overflow-y: visible;    
  }

  .error {
    margin-top: 10px;
    color: rgb(0, 0, 0);
    padding: 5px;
    border:2px solid rgb(255, 0, 0);
    background: rgba(255, 0, 0, 0.678);
    border-radius:5px;
  }

  .input {
    margin-top: 20px;
  }

</style>