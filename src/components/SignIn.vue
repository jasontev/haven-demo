<template>
    <div>
        <nav class="navbar navbar-expand-lg">
            <h1 class="navbar-brand">BookFace</h1>
            <button class="btn btn-success" @click="authenticate">Login with Haven</button>
        </nav>
        <div class="jumbotron">
            <p>BookFace is a demo website that implements the Haven protocol.</p>
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
<style scoped>
.navbar {
    background-color: #3b5998;
}

.navbar-brand {
    color: white;
    font-size: 1.5em;
}
</style>

