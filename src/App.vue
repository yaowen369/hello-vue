<template>
  <div>
    <div>
      {{ message }}
    </div>

    <div id="app-2">
      <span v-bind:title="message2">
        鼠标悬停几秒钟查看此处动态绑定的提示信息！
      </span>
    </div>

    <div id="app-5">
      <button v-on:click="reverseMessage">反转消息</button>
    </div>

    <div class="split"> app-6 </div>
    <div id="app-6">
      <input v-model="message" placeholder="edit me">
      <p>输入的message is： {{message}}</p>
    </div>

    <div class="split"> app-7 </div>
    <div id="app-7">
      <span>Multiline message is:</span>
      <p style="white-space: pre-line">{{message}}</p>
      <br>
      <textarea v-model="message" placeholder="add multiple lines"></textarea>
    </div>


    <div class="split"> app-8 </div>
    <div id="app-8">
      <input type="checkbox" id="jack" value="Jack" v-model="checkedNames">
      <label for="jack">Jack</label>

      <input type="checkbox" id="john" value="John" v-model="checkedNames">
      <label for="john">John</label>

      <input type="checkbox" id="mike" value="Mike" v-model="checkedNames">
      <label for="mike">Mike</label>

      <br>
      <span>Checked names: {{ checkedNames }}</span>
    </div>

    <div class="split"> app-9 </div>
    <div id="app-9">
      <input type="radio" id="one" value="One" v-model.lazy="picked">
      <label for="one">One</label>
      <br>
      <input type="radio" id="two" value="Two" v-model.trim="picked">
      <label for="two">Two</label>
      <br>
      <span>Picked: {{picked}}</span>
    </div>

    <div class="split"> app-10 </div>

    <div>{{ loginType === 'username' }}</div>
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

    <div class="split"> app-11 </div>
    <div id="app-11">
      <select v-model="selected">
        <option v-for="option in options" v-bind:value="option.value">
          {{option.text}}
        </option>
      </select>
      <span>Selected: {{ selected }}</span>
    </div>

    <div class="split"> app-12 </div>
    <ul id="app-12">
      <li v-for="(value, key, index) in object">
        ～ {{ value }} -- {{key}} -- {{index}}
      </li>
    </ul>

    <div class="split"> app-13 </div>
    <ul id="app-13">
      <li v-for="n in eventNumbers">
        {{ n }}
      </li>
    </ul>

    <div class="split"> app-14</div>
    <ul id="app-14" v-for="set in sets">
      <li v-for="n in even(set)">{{n}}</li>
    </ul>

    <div class="split"> app-15</div>
    <div id="app-15">
      <span v-for="n in 10">{{n}}</span>
    </div>


    <div class="split"> app-16</div>
    <div id="app-16">
      <button @click.stop="say('hii')">say hi</button>
      <button @click="say('what')">say what</button>
    </div>


    <div class="split"> app-17</div>
    <div id="app-17">
      <button @click.once="warn('Form cannot be summitted yet', $event)">Submit</button>
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
      count:0,
      message: '',
      message2: '页面加载于 ' + new Date().toLocaleString(),
      isActive: 0.0,
      errorClass: '',
      activeColor: 'red',
      fontSize: 10,
      loginType: '',
      items: [
        {message: 'FOO1'},
        {message: 'Baz'},
        {message: 'BAR'},

      ],
      object : {
        publish : '中国文艺出版社',
        author: '刘慈欣',
        title: '《三体》',
      },
      numbers: [1, 2, 3, 4, 5],
      sets:[[1, 2, 3, 4, 5], [6, 7, 8, 9, 10]],
      checkedNames:[ ],
      picked:null,
      selected:'',
      options: [
        {text: 'One', value: 'A'},
        {text: 'Two', value: 'B'},
        {text: 'Three', value: 'C'},
      ],
    }
  },

  beforeCreate: function () {
    console.log('生命周期函数, beforeCreate' + "," + this);
  },
  mounted: function () {
    console.log('生命周期函数, mounted' + "," + this);
  },
  created: function () {
    console.log('生命周期函数, created' + "," + this);
  },

  updated: function () {
    console.log('生命周期函数, updated');
  },
  destroyed: function () {
    console.log('生命周期函数, destroyed');
  },
  methods: {
    switchLogin: function () {
      this.loginType = (this.loginType === 'username') ? 'emal' : 'username';
    },
    even: function (numbers) {
      return numbers.filter(function (number){
        return number % 2 === 0
      })
    },
    greet: function (event) {
      alert('hello' + this.name + "!")
      if (event) {
        alert(event.target.id + event.target.tagName + event.target.key)
      }
    },
    say:function (msg) {
      alert(`say ${msg}`)
    },
    warn:function (msg, event) {
      console.log("1,warn: " + event)
      console.log("2,warn: " + JSON.stringify(event))
      if (event) {
        event.preventDefault()
      }
      alert(msg)
    }
  },

  computed: {
    reverseMessage: function () {
      console.log('计算属性 computed, ');
      return this.message.split('').reverse().join('')
    },
    styleObject: function () {
      return {
        color: `blue`,
        fontSize: '45px'
      }
    },
    eventNumbers:function () {
      return this.numbers.filter(function (number) {
        return number % 2 === 0
      })
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

.split {
  background: #42b983;
  font-weight: bold;
}
</style>
