<template>
    <div class="container">
        <div class="jumbotron">
            <h1>Sign in thing</h1>
            <button class="button" @click="authenticate">sign in</button>
        
        </div>
    </div>
</template>

<script>
import io from 'socket.io-client'
const socket = io('http://localhost:4242')

export default {
  name: 'SignIn',
  mounted () {
      socket.open()
  },
  methods: {
      authenticate() {
          socket.emit('auth', {
              origin: window.location.origin,
              permissions: ['name', 'email']
          });
      }
  }
}
</script>
