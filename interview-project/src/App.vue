<template>
  <div id="app">
    <!-- <nav>
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </nav> -->
    <van-tabbar v-model="active">
      <van-tabbar-item icon="home-o" @click="routerPush('/')">标签</van-tabbar-item>
      <van-tabbar-item icon="search" @click="routerPush('/about')">标签</van-tabbar-item>
      <van-tabbar-item icon="friends-o">标签</van-tabbar-item>
    </van-tabbar>
    <keep-alive>
    <router-view />

    </keep-alive>
  </div>
</template>
<script>
export default {
  data() {
    return {
      active: 0,
    };
  },
  methods:{
    routerPush(path){
      this.$router.push(path)
    }
  }
};
</script>
<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
