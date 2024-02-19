<template>
  <section class="jumbotron">
    <h3 class="jumbotron-heading">Search Github Users</h3>
    <div>
      <input
        type="text"
        placeholder="enter the name you search"
        v-model="input"
      />&nbsp;
      <button @click="search">Search</button>
    </div>
  </section>
</template>

<script>
import axios from 'axios'
export default {
  name: 'MySearch',
  data() {
    return {
      input: '',
    }
  },
  methods: {
    async search() {
      //firstSearching
      this.$bus.$emit('getData', {
        users: [],
        isFirstSearching: false,
        isLoading: true,
        errorMessage: '',
      })
      await axios
        .get(
          `https://api.github.com/search/users?q=${this.input}`
        )
        .then(
          //请求成功时的页面
          (res) => {
            this.$bus.$emit('getData', {
              users: res.data.items,
              isLoading: false,
              errorMessage: '',
            })
          },
          //请求失败时的页面
          (err) =>
            this.$bus.$emit('getData', {
              errorMessage: err.message,
              users: [],
            })
        )
    },
  },
}
</script>

<style></style>
