<template>
  <div class="row">
    <!-- 渲染用户信息 -->
    <div
      v-show="status.users.length"
      class="card"
      v-for="user in status.users"
      :key="user.login"
    >
      <a :href="user.html_url" target="_blank">
        <img :src="user.avatar_url" style="width: 200px" />
      </a>
      <p class="card-text">{{ user.login }}</p>
    </div>
    <!-- welcome -->
    <h1 v-show="status.isFirstSearching">welcome</h1>
    <!-- loading -->
    <h1 v-show="status.isLoading">loading...</h1>
    <!-- error -->
    <h1 v-show="status.errorMessage">
      {{ status.errorMessage }}
    </h1>
  </div>
</template>

<script>
export default {
  name: 'MyList',
  data() {
    return {
      status: {
        //是否是初次使用
        isFirstSearching: true,
        //是否正在加载数据
        isLoading: false,
        //错误信息
        errorMessage: '',
        //数据存放于此
        users: [],
      },
    }
  },
  methods: {
    getData(options) {
      console.log('收到组件内通信数据')
      this.status = { ...this.info, ...options }
    },
  },
  mounted() {
    this.$bus.$on('getData', this.getData)
  },
}
</script>

<style scoped>
.album {
  min-height: 50rem; /* Can be removed; just added for demo purposes */
  padding-top: 3rem;
  padding-bottom: 3rem;
  background-color: #f7f7f7;
}

.card {
  float: left;
  width: 33.333%;
  padding: 0.75rem;
  margin-bottom: 2rem;
  border: 1px solid #efefef;
  text-align: center;
}

.card > img {
  margin-bottom: 0.75rem;
  border-radius: 100px;
}

.card-text {
  font-size: 85%;
}
</style>
