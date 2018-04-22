<template>
    <div>
        <nav class="navbar navbar-expand-lg">
            <h1 class="navbar-brand"><a href="/" class="text-white">BookFace</a></h1>
            <input class="form-control" placeholder="Search Placeholder"/>
        </nav>
        <div class="jumbotron">
            <h1>Welcome back, {{ $route.query.data.name }}</h1>
            <p>All the info we have:</p>
            <ul>
                <li>{{ $route.query.data.name }}</li>
                <li>{{ $route.query.data.email }}</li>
                <li>public key fingerprint <code>0x{{ $route.query.fingerprint.toUpperCase() }}</code></li>                
            </ul>
            <code>{{ $route.query.pubkey }}</code>
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
.navbar {
    background-color: #3b5998;
}

.navbar-brand {
    color: white;
    font-size: 1.5em;
}

code {
    white-space: pre;
}
</style>
