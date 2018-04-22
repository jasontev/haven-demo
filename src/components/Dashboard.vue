<template>
    <div>
        <nav class="navbar navbar-expand-lg">
            <h1 class="navbar-brand"><a href="/" class="text-white">T0t4lly S3cure B4nk1ng</a></h1>
        <img src="https://proxy.duckduckgo.com/iu/?u=https%3A%2F%2Fwww.freebie-depot.com%2Fwp-content%2Fuploads%2F2015%2F04%2F20-Free.jpg&f=1" alt="">
        <img src="https://proxy.duckduckgo.com/iu/?u=https%3A%2F%2Fwww.freebie-depot.com%2Fwp-content%2Fuploads%2F2015%2F04%2F20-Free.jpg&f=1" alt="">
        <img src="https://proxy.duckduckgo.com/iu/?u=https%3A%2F%2Fwww.freebie-depot.com%2Fwp-content%2Fuploads%2F2015%2F04%2F20-Free.jpg&f=1" alt="">
        </nav>
        <div class="jumbotron">
            <h3>MWAHAHAHA, <i>{{ $route.query.data.name }}</i>!<br>
                WE HAVE THE NAME YOU GAVE US (i.e. "{{ $route.query.data.name }}") AND...<br>your <mark>public</mark> key[1] :/</h3>
            <p>Well THAT sucks (for us)</p>
            <p>[1] <code>0x{{ $route.query.fingerprint }}</code></p>
        </div>
    </div>
</template>

<script>
import io from 'socket.io-client'
const socket = io('http://localhost:4242')

export default {
  name: 'SignIn',
  data () {
      return {
          foo: {},
          pubkey: '',
          fingerprint: ''
      }
  },
  mounted () {
      socket.open()

    socket.on('authenticated', (data) => {
        console.log(data)
        this.pubkey = data.pubkey
        this.fingerprint = data.fingerprint
    })

    socket.on('permissionData', (data) => {
        console.log(data)
        this.foo = data
        console.log(this)
    })
  },
  computed: {
      username() {
          return ''
      },
      email() {
          return ''
      }
  },
  methods: {
      foo () {
          
      }
  }
}
</script>

<style scoped>
code {
    white-space: pre;
    color: lawngreen;
    background-color: black;
}

.navbar {
    background-color: #48ff00;
}

.navbar-brand {
    color: red;
    font-size: 1.5em;
}

button {
    background-color: blue;
    color: white;
}

img {
    width: 10%
}
</style>
