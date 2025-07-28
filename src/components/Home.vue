<template>
  <div class="home">
    <h3>首页组件</h3>
    <p>{{ message }}</p>
    <button @click="changeMessage">修改消息</button>
  </div>
</template>


<script>
export default {
  name: "Home",
  props: ['message'],
  methods: {
    changeMessage: function () {
      this.$emit('update-message', '首页修改了这条message')
    }
  }
}
</script>


<style scoped>
  .home {
    color: #333;
  }
</style>
