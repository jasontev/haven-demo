<template>
    <div class="container">
        <div class="jumbotron">
            <h1>Sign in thing</h1>
            <button class="btn btn-success" @click="authenticate">sign in</button>
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

    socket.on('authenticated', (data) => {
        console.log(data)
        // alert('authenticated ')
    })
    socket.on('permissionData', (data) => {
        console.log(data)
        // alert('authenticated ')
    })
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
