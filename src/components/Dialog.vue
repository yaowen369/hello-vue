<template>
  <div class="dialog">
    <div class="header">
      <!--  默认插槽 -->
      <slot>默认标题</slot>
    </div>

    <div class="content">
      <!--  具名插槽    -->
      <slot name="content">默认内容</slot>
    </div>

    <div class="footer">
      <!--  作用域插槽     -->
      <slot name="footer" :closeDialog="closeDialog2">默认footer</slot>
    </div>
  </div>
</template>


<script>
export default {
  name: "Dialog",
  methods: {
    closeDialog2() {
      console.log("关闭对话框")
    }
  }
}
</script>


<style scoped>
.dialog {
  padding: 20px;
  border: 1px solid #ccc;
  width: 300px;
  margin: auto;
}

.header {
  background-color: #f5f5f5;
  padding: 10px;
  text-align: center;
}

.content {
  padding: 20px;
  text-align: center;
}

.footer {
  text-align: right;
  padding: 10px;
}
</style>
