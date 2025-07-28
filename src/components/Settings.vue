<template>
  <div class="settings">
    <h3>设置组件</h3>
    <p>{{message}}</p>
    <div>
      <label>
        <input type="checkbox" v-model="notifications">
        接收通知
      </label>
    </div>
  </div>
</template>


<script>
export default {
  name: "Settings",
  props:['message'],
  data() {
    return {
      notifications:true
    }
  }
}
</script>



<style scoped>
  .settings {
    color: #999;
  }
</style>
