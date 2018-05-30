<template>
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
    <button class="button" v-on:click="treechange">JSON to Tree</button>
    <button class="button" v-on:click="jsonchange" >Tree to JSON</button>
    <div class="jsontree">
      <tree-view v-model="mydata" :data="mydata" :options="{maxDepth: 3, modifiable: true, rootObjectKey: 'Your JSON'}" @change-data="onChangeData" ></tree-view>
    </div>
  </div>
</template>

<script>
import Treeview from 'vue-json-tree-view'
import Vue from 'vue'

Vue.use(Treeview)
export default {
  props: [
    'myjson'
  ],
  data: function () {
    return {
      lines: 0,
      mydata: {}
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
      this.$emit('update', this.myjson)
    },
    jsonchange: function () {
      console.log(this.myjson)
      this.myjson = JSON.stringify(this.mydata)
      console.log(this.myjson)
      this.$emit('update', this.myjson)
    },
    treechange: function () {
      this.mydata = JSON.parse(this.myjson, null, 2)
    },
    onChangeData: function (datas) {
      this.mydata = datas
    }
  }
}
</script>

<style>

textarea {
  background-color: rgb(212, 215, 232);
  padding: 3px;
  border: 1px solid rgba(0, 102, 255, 0.514);
  border-block-start-color: blue;
  height: 611px;
  width: 40%;
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

.jsontree {
  background-color: rgb(212, 215, 232);
  padding: 3px;
  border: 1px solid rgba(0, 102, 255, 0.514);
  border-block-start-color: blue;
  height: 611px;
  width: 40%;
  resize: none;
  overflow: hidden;
  display: inline-block;
  margin-left: -10px;
  font-size: 16px;
  line-height: 20px;
  font-family: "Source Sans Pro", sans-serif;
}

textarea:focus {
  caret-color: #21abfa;
  overflow: visible;
}

#myscroll {
  background-color: rgb(195, 198, 211);
  font-family: "Source Sans Pro", sans-serif;
  font-size: 16px;
  line-height: 20px;
  color: rgb(99, 51, 187);
  float: left;
  margin-left: 0%;
  padding-top: 4px;
  padding-left: 22px;
  padding-bottom: 9px;
  width: 45px;
  height: 606px;
  scroll-behavior: unset;
  overflow: hidden;
}


.button {
  font-family: "Source Sans Pro", sans-serif;
	border:none;
	padding:6px 0 6px 0;
	border-radius:75%;
	border-bottom:7px solid #4753f3;
	font:bold 13px Arial;
	color:#555;
	background:#fff;
	box-shadow:2px 2px 3px #999;
	border-top:2px solid #59cd27;
}

</style>
