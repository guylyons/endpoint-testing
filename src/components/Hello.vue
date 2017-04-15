<template>
  <div class="hello">
    <ul>
      <li v-for="post in posts">{{ post.title }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      posts: []
    }
  },
  mounted: function () {
    var that
    that = this
    var root = 'https://jsonplaceholder.typicode.com'
    var httpRequest = new XMLHttpRequest()

    httpRequest.onreadystatechange = responseReady

    httpRequest.open('GET', root + '/posts', true)
    httpRequest.send()

    function responseReady () {
      if (httpRequest.readyState === XMLHttpRequest.DONE) {
        if (httpRequest.status === 200) {
          var response = JSON.parse(httpRequest.responseText)
          that.posts = response
        } else {
          alert('There was a problem with the request.')
        }
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
