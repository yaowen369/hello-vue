<template>
  <div id="app">
    <div>
      {{message}}
    </div>

    <div id="app-2">
      <span v-bind:title="message2">
        鼠标悬停几秒钟查看此处动态绑定的提示信息！
      </span>
    </div>

    <div id="app-5">
      <button v-on:click="reverseMessage">反转消息</button>
    </div>

    <div id="app-6">
      <p>message</p>
      <input v-model="message">
    </div>

    <div id="app-7">
      <p>通过计算属性,来自动的反转message : {{reverseMessage}}</p>
    </div>

    <div id="app-8"
         :class="[{active: isActive}, errorClass]"
    >
      测试class的绑定
    </div>

    <div id="app-9"
      :style="styleObject"
    >
      测试style的绑定
    </div>

    <div>{{loginType === 'username'}}</div>
    <div style="background:yellow; display: flex; flex-direction: column">
      <template v-show="loginType === 'username'">
        <label>UserName</label>
        <input placeholder="enter your username" key="username-key"/>
      </template>
      <template>
        <label>Email</label>
        <input placeholder="enter your email" key="email-key"/>
      </template>
      <button @click="switchLogin">切换登录方式</button>
    </div>



<!--    这个组件始终没有引用成功，还没找到原因 -->
<!--    <ol>-->
<!--      <todo-item></todo-item>-->
<!--    </ol>-->
<!--    <HelloWorld msg="Welcome to Your Vue.js App"/>-->
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';
import TodoItem from "./components/TodoItem.vue";

export default {
  name: 'App',
  data() {
    return {
      message: 'Hello Vue!',
      message2: '页面加载于 ' + new Date().toLocaleString(),
      isActive: 0.0,
      errorClass: '',
      activeColor: 'red',
      fontSize: 10,
      loginType:''
    }
  },

  beforeCreate:function () {
    console.log('生命周期函数, beforeCreate'+ "," + this);
   },
  mounted: function () {
    console.log('生命周期函数, mounted'+ "," + this);
  },
  created: function () {
    console.log('生命周期函数, created' + "," + this);
  },

  updated:function () {
    console.log('生命周期函数, updated');
   },
  destroyed:function () {
    console.log('生命周期函数, destroyed');
   },
  methods: {
    switchLogin:function () {
      this.loginType = (this.loginType==='username') ? 'emal' : 'username';
    }
  },

  computed: {
    reverseMessage: function () {
      console.log('计算属性 computed, ');
      return  this.message.split('').reverse().join('')
    },
    styleObject: function (){
      return {
        color:`blue`,
        fontSize:'45px'
      }
    }
  },
  components: {
    TodoItem,
    HelloWorld
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}


.active {
  font-size: 40px;
}

.text-danger {
  color: red;
}
</style>
