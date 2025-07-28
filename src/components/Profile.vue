<template>
  <div class="profile">
    <h3>个人资料组件</h3>
    <p>{{message}}</p>
    <div>
      <label>姓名:</label>
      <input type="text" v-model="name">
    </div>
  </div>
</template>

<script>
export default {
  name: "Profile",
  props:['message'],
  data(){
    return {
      name: '张三'
    }
  }
}
</script>



<style scoped>
 .profile {
   color: #666;
 }
 input {
   margin-top: 10px;
   padding: 5px;
 }
</style>
