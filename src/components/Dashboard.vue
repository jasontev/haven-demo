<template>
    <div>

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
        alert('authenticated ')
    })
  },
  computed: {
      username() {
          return ''
      },
      email() {
          return ''
      }
  }
  methods: {
      foo () {
          
      }
  }
}
</script>
