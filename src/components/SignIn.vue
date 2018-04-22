<template>
    <div>
        <nav class="navbar navbar-expand-lg">
            <h1 class="navbar-brand">T0t4lly S3cure B4nk1ng</h1>
        <img src="https://proxy.duckduckgo.com/iu/?u=https%3A%2F%2Fwww.freebie-depot.com%2Fwp-content%2Fuploads%2F2015%2F04%2F20-Free.jpg&f=1" alt="">
            <button class="btn btn-success" @click="authenticate">Login with Haven</button>
        </nav>
    </div>
</template>

<script>
import io from 'socket.io-client'
const socket = io('http://localhost:4242')

export default {
  name: 'SignIn',
  data () {
      return {
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
        this.$router.replace({path: '/dashboard', query: { data: data, pubkey: this.pubkey, fingerprint: this.fingerprint }})
    })
  },
  methods: {
      authenticate() {
          socket.emit('auth', {
              origin: window.location.origin,
              permissions: ['name']
          });
      }
  }
}
</script>
<style scoped>
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

