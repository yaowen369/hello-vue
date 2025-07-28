<template>
  <div>
    <div id="app-1">
      <button-counter></button-counter>
    </div>


    <div class="split"> app-2</div>
    <div id="app-2" :style="{fontSize: postFontSize + 'em'}">
      <blog-post
          v-for="post in posts"
          :key="post.id"
          v-on:enlarge-text="onEnlargeText"
          :post="post">
      </blog-post>
    </div>

    <div class="split"> app-5</div>
    <div id="app-5">
      <!--  动态组件     -->
      <component :is="currentComponent"></component>

      <!--   按钮用于切换组件   -->
      <button @click="currentComponent='ComponentA'">加载组件A</button>
      <button @click="currentComponent='ComponentB'">加载组件B</button>
      <button @click="currentComponent='ComponentC'">加载组件C</button>

    </div>

    <div class="split"> app-6</div>
    <div id="app-6" class="dynamic-component-demo">
      <h2>Vue2 动态组件实例</h2>
      <!--      按钮组，用于切换不同的组件 -->
      <div class="button-group">
        <button
            v-for="(component, index) in components"
            :key="index"
            @click="currentComponent = component.name"
            :class="{active:currentComponent === component.name}"
        >
          {{ components.label }}
        </button>
      </div>

      <!--      动态组件挂载点 -->
      <div class="component-container">
        <keep-alive>
          <component
              :is="currentComponent"
              :message="message"
              @update-message="updateMessage"
          ></component>
        </keep-alive>
      </div>


      <!--       显示当前组件信息 -->
      <div class="info">
        <p>当前显示的组件: {{ currentComponent }}</p>
        <p>共享消息: {{ message }}</p>
      </div>

    </div>


    <div class="split"> app-8 slot插槽的使用</div>
    <div id="app-8">
      <Dialog>
        <span style="background: blue"> 自定义标题</span>
        <template slot="content">
          <div style="background: red; color: yellow">
            这是自定义的内容部分
          </div>
        </template>
        <template slot="footer" slot-scope="props">
          <button @click="props.closeDialog()">关闭</button>
        </template>
       <span style="color: aqua">自定义标题的下面  222 </span>
      </Dialog>
    </div>

    <div class="split"> app-9</div>
    <div id="app-9">
      <input type="radio" id="one" value="One" v-model.lazy="picked">
      <label for="one">One</label>
      <br>
      <input type="radio" id="two" value="Two" v-model.trim="picked">
      <label for="two">Two</label>
      <br>
      <span>Picked: {{ picked }}</span>
    </div>

    <div class="split"> app-10</div>

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

    <div class="split"> app-11</div>
    <div id="app-11">
      <select v-model="selected">
        <option v-for="option in options" v-bind:value="option.value">
          {{ option.text }}
        </option>
      </select>
      <span>Selected: {{ selected }}</span>
    </div>

    <div class="split"> app-12</div>
    <ul id="app-12">
      <li v-for="(value, key, index) in object">
        ～ {{ value }} -- {{ key }} -- {{ index }}
      </li>
    </ul>

    <div class="split"> app-13</div>
    <ul id="app-13">
      <li v-for="n in eventNumbers">
        {{ n }}
      </li>
    </ul>

    <div class="split"> app-14</div>
    <ul id="app-14" v-for="set in sets">
      <li v-for="n in even(set)">{{ n }}</li>
    </ul>

    <div class="split"> app-15</div>
    <div id="app-15">
      <span v-for="n in 10">{{ n }}</span>
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
import ButtonCounter from "./components/ButtonCounter.vue";
import BlogPost from "./components/BlogPost.vue";
import ComponentA from "./components/ComponentA.vue";
import ComponentB from "./components/ComponentB.vue";
import ComponentC from "./components/ComponentC.vue";
import Home from "./components/Home.vue";
import Profile from "./components/Profile.vue";
import Settings from "./components/Settings.vue";
import Dialog from "./components/Dialog.vue";

export default {
  name: 'App',
  data() {
    return {
      count: 0,
      message: '这是一条共享信息',
      currentComponent: 'Home',
      components: [
        {name: 'Home', label: '首页'},
        {name: 'Profile', label: '个人资料'},
        {name: 'Settings', label: '设置'},
      ],
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
      object: {
        publish: '中国文艺出版社',
        author: '刘慈欣',
        title: '《三体》',
      },
      numbers: [1, 2, 3, 4, 5],
      sets: [[1, 2, 3, 4, 5], [6, 7, 8, 9, 10]],
      picked: null,
      selected: '',
      options: [
        {text: 'One', value: 'A'},
        {text: 'Two', value: 'B'},
        {text: 'Three', value: 'C'},
      ],
      posts: [
        {id: 1, title: 'Blog title1', content: 'Content1'},
        {id: 2, title: 'Blog title2', content: 'Content2'},
        {id: 3, title: 'Blog title3', content: 'Content3'}
      ],
      postFontSize: 1,

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
      return numbers.filter(function (number) {
        return number % 2 === 0
      })
    },
    greet: function (event) {
      alert('hello' + this.name + "!")
      if (event) {
        alert(event.target.id + event.target.tagName + event.target.key)
      }
    },
    say: function (msg) {
      alert(`say ${msg}`)
    },
    warn: function (msg, event) {
      console.log("1,warn: " + event)
      console.log("2,warn: " + JSON.stringify(event))
      if (event) {
        event.preventDefault()
      }
      alert(msg)
    },
    onEnlargeText: function (enlargeAmount) {
      this.postFontSize += enlargeAmount
    },
    updateMessage: function (newMsg) {
      this.message = newMsg
    }
  },

  computed: {
    styleObject: function () {
      return {
        color: `blue`,
        fontSize: '45px'
      }
    },
    eventNumbers: function () {
      return this.numbers.filter(function (number) {
        return number % 2 === 0
      })
    }
  },
  components: {
    Dialog,
    BlogPost,
    ButtonCounter,
    TodoItem,
    HelloWorld,
    ComponentA,
    ComponentB,
    ComponentC,
    Home,
    Profile,
    Settings
  }
};
</script>

<style scoped>
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

.dynamic-component-demo {
  max-width: 800px;
  margin: 20px auto;
  padding: 20px;
  font-family: Arial, sans-serif;
}

.button-group {
  margin-bottom: 20px;
  display: flex;
  gap: 10px;
}

button {
  padding: 8px 16px;
  cursor: pointer;
  border: 1px solid #ccc;
  background-color: #fff;
  border-radius: 4px;
  transition: all 0.3s;
}

button.active {
  background-color: #42b983;
  color: white;
  border-color: #42b983;
}

.component-container {
  border: 1px solid #eee;
  padding: 20px;
  min-height: 150px;
  margin-bottom: 20px;
  border-radius: 4px;
}

.info {
  color: #666;
  font-size: 0.9em;
  padding: 10px;
  background-color: #f9f9f9;
  border-radius: 4px;
}
</style>
