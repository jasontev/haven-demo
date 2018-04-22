<template>
    <div>
        {{ data }}
    </div>
</template>

<script>
import io from 'socket.io-client'
const socket = io('http://localhost:4242')

export default {
  name: 'SignIn',
  data () {
      return {
          data: {}
      }
  },
  mounted () {
      socket.open()

    socket.on('authenticated', (data) => {
        console.log(data)
    })

    socket.on('permissionData', (data) => {
        this.data = data
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
