<template>
  <div>
    {{ posts }}
  </div>
</template>

<script>
import axios from 'axios'

export default {

  data () {
    return {
      posts: []
    }
  },

  async created () {
    const response = await axios.get('https://jsonplaceholder.typicode.com/posts')
    this.posts = response.data
  }
}
</script>
