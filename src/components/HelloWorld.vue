<template>
  <div class="hello">
    <h1 style="text-algin: center"> Welcome To Scan DashBoard.</h1>
    <label> IP/IPrange: </label> <input v-model="ip"> 
    <button @click="steamIT">startScan</button>
    <pre> <div class="magin_5px"> {{ msg }} </div> </pre>
    <ul>
    </ul>
  </div>
</template>

<script>
// const axios = require('axios')
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: "",
      ip: "",
    }
  },
  mounted () {
    // this.steamIT()
  },
  methods: {
    steamIT: function () {
      this.msg = ""
      var xhr = new XMLHttpRequest()
      xhr.open('GET', '/tools/test?ip='+this.ip)
      xhr.seenBytes = 0
      var that = this;
      xhr.onreadystatechange = function () {
        console.log('state change.. state: ' + xhr.readyState)
        if (xhr.readyState === 3) {
          var newData = xhr.response.substr(xhr.seenBytes)
          that.msg += newData
          xhr.seenBytes = xhr.responseText.length
          console.log('seenBytes: ' + xhr.seenBytes)
        }
      }
      xhr.addEventListener('error', function (e) {
        console.log('error: ' + e)
      })
      console.log(xhr)
      xhr.send()
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
 pre {
   background: #bfe6ff;
 }
button {
  background: #3498db;
  width: 150px;
  padding: 4px 0;
  border-radius: 5px;
}
.magin_5px { 
  padding-left: 20px
}
</style>
