<template>
  <div class="search">
    <input v-model="searchQuery" @keyup.enter="search"/>
  </div>
</template>

<script>
import axios from 'axios'

const BASE_URL = `http://www.omdbapi.com/?i=tt3896198&apikey=7d453a07`

export default {
  name: 'search',
  data () {
    return {
      searchQuery: ''
    }
  },
  methods: {
    async search () {
      let response = await axios.get(`${BASE_URL}&s=${this.searchQuery}`)
      if (response.status === 200) {
        let data = response.data
        if (data.Response === 'True') {
          return this.$emit('search', data.Search)
        }
      }
    }
  }
}
</script>

<style>
</style>
