<template>
    <div class="container">
        <div class="jumbotron">
            <h1>BookFace</h1>
            <button class="btn btn-success" @click="authenticate">Login with Haven</button>
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
        this.$router.replace('/dashboard')
    })
    socket.on('permissionData', (data) => {
        // console.log(data)
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
