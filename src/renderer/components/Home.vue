<template>
  <div id="wrapper">
    <Header></Header>
    <div>
      <!-- used ref as in API https://vuejs.org/v2/api/  -->
      <div id="myscroll" v-on:scroll="keymonitor" ref="myscroll">
        0 <br>
        <span v-for="line in lines"> {{line}} <br> </span>
        <br>
      </div>
      <textarea v-model="myjson" ref="text" id="text" type="text" placeholder="Place your JSON here"
        v-on:scroll="keymonitor" v-on:keyup="keymonitor" v-on:keydown="keymonitor">
      </textarea>
      <!-- <textarea v-model="result" type="text" placeholder="JSON Tree"
        v-on:scroll="keymonitor" v-on:keyup="keymonitor" v-on:keydown="keymonitor">
      </textarea> -->
    </div>
    <Footer :myjson="myjson" @update="onFooterUpdate"></Footer>
  </div>
</template>

<script type="text/javascript">
import Header from '@/components/MyHeader'
import Footer from '@/components/MyFooter'

export default {
  name: 'home',
  components: {
    Header,
    Footer
  },
  data: function () {
    return {
      myjson: '',
      lines: 0
    }
  },
  methods: {
    keymonitor: function (event) {
      if (this.$refs.text.value.match(/[\r\n]/g)) {
        this.lines = this.$refs.text.value.match(/[\r\n]/g).length
      } else {
        this.lines = 0
      }
      if (this.$refs.text.scrollTop != null) {
        this.$refs.myscroll.scrollTop = this.$refs.text.scrollTop + 2
      }
    },
    onFooterUpdate (newdata) {
      this.myjson = newdata
    }
  }
}
</script>

<style>

@import url("https://fonts.googleapis.com/css?family=Source+Sans+Pro");

body {
  font-family: "Source Sans Pro", sans-serif;
  overflow: hidden;
}

textarea {
  background-color: rgb(212, 215, 232);
  padding: 3px;
  border: 1px solid rgba(0, 102, 255, 0.514);
  border-block-start-color: blue;
  height: 611px;
  width: 500px;
  resize: none;
  overflow-y: hidden;
  overflow-x: hidden;
  display: inline-block;
  margin-left: -10px;
  font-size: 16px;
  line-height: 20px;
  font-family: "Source Sans Pro", sans-serif;
  wrap: off;
  white-space: pre;
}

textarea:focus {
  caret-color: #21abfa;
  overflow: visible;
}

#wrapper {
  height: 100vh;
  padding: 60px 80px;
  width: 100vw;
}

#myscroll {
  font-family: "Source Sans Pro", sans-serif;
  padding-top: 4px;
  background-color: rgb(195, 198, 211);
  color: rgb(99, 51, 187);
  width: 45px;
  height: 606px;
  float: left;
  padding-left: 25px;
  padding-bottom: 9px;
  font-size: 16px;
  line-height: 20px;
  scroll-behavior: unset;
  overflow: hidden;
}

</style>