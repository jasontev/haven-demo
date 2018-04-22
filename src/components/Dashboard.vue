<template>
    <div>
        <nav class="navbar navbar-expand-lg">
            <h1 class="navbar-brand"><a href="/" class="text-white">BookFace</a></h1>
            <input class="form-control" placeholder="Fancy search feature" @click="authenticate"/>
        </nav>
        <div class="jumbotron">
            <h1>Welcome back, {{ $route.query.data.name }}</h1>
            <p>Info we have:</p>
            <ul>
                <li>{{ $route.query.data.name }}</li>
                <li>{{ $route.query.data.email }}</li>
            </ul>
            <code>
                {{ pubkey }}
            </code>
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
          pubkey: ''
      }
  },
  mounted () {
      socket.open()

    socket.on('authenticated', (data) => {
        console.log(data)
        this.pubkey = data
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
</style>
