##### Vue是一套用于构建用户界面的渐进式框架。

- 声明式渲染
- 组件化应用构建

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<title></title>
		<!-- 开发环境版本，包含了有帮助的命令行警告 -->
		<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
	</head>
	<body>
		<div id="app">
		  {{ message }}
		</div>
		
		<div id="app-2">
		  <span v-bind:title="message">
		    鼠标悬停几秒钟查看此处动态绑定的提示信息！
		  </span>
		</div>
		
		<div id="app-3">
		  <p v-if="seen">现在你看到我了</p>
		</div>
		
		<div id="app-4">
		  <ol>
		    <li v-for="todo in todos">
		      {{ todo.text }}
		    </li>
		  </ol>
		</div>
		
		<div id="app-5">
		  <p>{{ message }}</p>
		  <button v-on:click="reverseMessage">反转消息</button>
		</div>
		
		<div id="app-6">
		  <p>{{ message }}</p>
		  <input v-model="message">
		</div>
		
		<div id="app-7">
		  <ol>
			    <!--
			      现在我们为每个 todo-item 提供 todo 对象
			      todo 对象是变量，即其内容可以是动态的。
			      我们也需要为每个组件提供一个“key”，稍后再
			      作详细解释。
			    -->
		    <todo-item
		      v-for="item in groceryList"
		      v-bind:todo="item"
		      v-bind:key="item.id"
		    ></todo-item>
		  </ol>
		</div>
		
		<script>
			var app = new Vue({
				  el: '#app',
				  data: {
				    message: 'Hello Vue!'
				  }
			})
			
			var app2 = new Vue({
				  el: '#app-2',
				  data: {
				    message: '页面加载于 ' + new Date().toLocaleString()
				  }
			})
			
			var app3 = new Vue({
				el: '#app-3',
					data: {
						seen : true
					}
			})
			
			var app4 = new Vue({
				 el: '#app-4',
				  data: {
				    todos: [
				      { text: '学习 JavaScript' },
				      { text: '学习 Vue' },
				      { text: '整个牛项目' }
				    ]
				  } 
			})
			
			var app5 = new Vue({
				  el: '#app-5',
				  data: {
				    message: 'Hello Vue.js!'
				  },
				  methods: {
				    reverseMessage: function () {
				      this.message = this.message.split('').reverse().join('')
				    }
				  }
			})
			
			var app6 = new Vue({
				  el: '#app-6',
				  data: {
				    message: 'Hello Vue!'
				  }
			})
			
			Vue.component('todo-item', {
			  props: ['todo'],
			  template: '<li>{{ todo.text }}</li>'
			})

			var app7 = new Vue({
			  el: '#app-7',
			  data: {
			    groceryList: [
			      { id: 0, text: '蔬菜' },
			      { id: 1, text: '奶酪' },
			      { id: 2, text: '随便其它什么人吃的东西' }
			    ]
			  }
			})
				</script>
	</body>
</html>
```

 `v-bind` attribute 被称为**指令**。指令带有前缀 `v-`，以表示它们是 Vue 提供的特殊 attribute 。

 `v-for` 指令可以绑定数组的数据来渲染一个项目列表 。

`v-on` 指令添加一个事件监听器，通过它调用在 Vue 实例中定义的方法。

 `v-model` 指令，它能轻松实现表单输入和应用状态之间的双向绑定 。

### **生命周期钩子**

 每个 Vue 实例在被创建时都要经过一系列的初始化过程——例如，需要设置数据监听、编译模板、将实例挂载到 DOM 并在数据变化时更新 DOM 等。同时在这个过程中也会运行一些叫做**生命周期钩子**的函数，这给了用户在不同阶段添加自己的代码的机会。 

[[https://cn.vuejs.org/v2/guide/instance.html#%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E5%9B%BE%E7%A4%BA](https://cn.vuejs.org/v2/guide/instance.html#生命周期图示) ]()]()

#### 模板语法