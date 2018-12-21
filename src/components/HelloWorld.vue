<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>Essential Links</h2>
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
      msg: 'Welcome to Your Vue.js App'
    }
  },
  mounted () {
    this.steamIT()
  },
  methods: {
    steamIT: function () {
      var xhr = new XMLHttpRequest()
      xhr.open('GET', '/tools/test')
      xhr.seenBytes = 0
      xhr.onreadystatechange = function () {
        console.log('state change.. state: ' + xhr.readyState)
        if (xhr.readyState === 3) {
          var newData = xhr.response.substr(xhr.seenBytes)
          console.log('newData: <<' + newData + '>>')
          document.body.innerHTML += 'New data: <<' + newData + '>><br />'
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
</style>
