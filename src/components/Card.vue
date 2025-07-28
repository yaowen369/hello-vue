<template>
  <div class="card">
    <div class="card-header">
      <slot name="header">默认标题</slot>
    </div>

    <slot></slot>
    <div class="card-list">
      <div v-for="(item, index) in userInfo" :key="index">
        <slot name="list"
              :item2="item"
        >
        </slot>
      </div>
    </div>
    <div class="card-footer">
      <slot name="footer">默认底部</slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "MyCard",
  data() {
    return {
      userInfo: [
        {label: '姓名', value: '张三'},
        {label: '年龄', value: '28'},
        {label: '姓名', value: '张三'},
      ]
    }
  }
}
</script>


<style scoped>
.card {
  width: 300px;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  padding: 16px;
  margin: 20px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.card-header {
  border-bottom: 1px solid #e0e0e0;
  padding-bottom: 8px;
  margin-bottom: 8px;
}

.card-footer {
  border-top: 1px solid #e0e0e0;
  padding-top: 8px;
  margin-top: 8px;
  text-align: right;
}

.card-list {
  margin: 12px 0;
  padding: 8px;
  background-color: #f9f9f9;
  border-radius: 4px;
}


</style>
