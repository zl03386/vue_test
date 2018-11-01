## 完整使用vue应会的知识：
```
1. HTML
2. CSS（css2,css3,css预处理器）
3. ES5
4. ES6
5. js模块化
6. node.js
7. 构建工具（webpack）
```

## vue简介
```
Vue.js是什么?
	一位华裔前Google工程师(尤雨溪)开发的前端js库
	作用: 动态构建用户界面的渐进式框架
特点:
	遵循MVVM模式
	编码简洁, 体积小, 运行效率高, 移动/PC端开发
	它本身只关注UI, 可以轻松引入vue插件和其它第三库开发项目
与其它框架的关联:
	借鉴angular的模板和数据绑定技术
	借鉴react的组件化和虚拟DOM技术
vue包含一系列的扩展插件(库):
	vue-cli: vue脚手架
	vue-resource(axios): ajax请求
	vue-router: 路由
	vuex: 状态管理
	vue-lazyload: 图片懒加载
	vue-scroller: 页面滑动相关
	mint-ui: 基于vue的组件库(移动端)
	element-ui: 基于vue的组件库(PC端)
对渐进式的理解：
	它是渐进的，没有强主张，
	你可以在原有大系统的上面，把一两个组件改用它实现，当jQuery用；
	也可以整个用它全家桶开发，当Angular用；
	还可以用它的视图，搭配你自己设计的整个下层用。

```

## 编码方式：
```
命令式编码： 如jQuery,zpto等
声明式编码： MVVM框架，如vue
```

## MVVM
```
MVVM是Model-View-ViewModel的简写
MVVM 可以使我们的代码更专注于处理业务逻辑，而不是去关心DOM 操作
在MVVM中，数据是核心，由于VIewModel与View之间的双向绑定，
	操作了ViewModel中的数据（当然只能是监控属性），就会同步到DOM，
	我们透过DOM事件监控用户对DOM的改动，也会同步到ViewModel。
Model:模型（本质：数据对象data）
View:视图（模板页面）
ViewModel:视图模型（本质vue实例）（包含dom listeners, data bindings）
```

## vue的基本使用：
```
1). 引入vue.js
2). 创建Vue实例对象(vm), 指定选项(配置)对象
		el : 指定dom标签容器的选择器
		data : 指定初始化状态数据的对象/函数(返回一个对象)
3). 在页面模板中使用{{}}或vue指令
```

## vue使用实例：
```
// 引入vue库
<script type="text/javascript" src="../js/vue.js"></script>

// js文件中创建vue对象，并配置
const vm = new Vue({
	// 配置选项(option)
	el: '#test',  // element: 指定用vue来管理页面中的哪个标签区域
	data: { // vm管理区域的数据
	}，
	methods: { // 包含多个方法的对象，供页面中的事件指令来绑定回调
	}，
	computed: { // 包含多个方法的对象,对状态属性进行计算返回一个新的数据, 供页面获取显示
	},
	watch: { // 包含多个属性监视的对象,分为一般监视和深度监视
					 // 另一种添加监视方式: vm.$watch('xxx', funn)
	}
})
```

## vue的引入：
```
Vue 不支持 IE8 及以下版本。

1. cdn远程引入：
	<!-- 开发环境版本，包含了有帮助的命令行警告 -->
	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

	<!-- 生产环境版本，优化了尺寸和速度 -->
	<script src="https://cdn.jsdelivr.net/npm/vue"></script>

2. 直接下载并用 <script> 标签引入，Vue 会被注册为一个全局变量。

3. 使用vue-cli搭建vue项目
		git clone https://github.com/vuejs/vue.git node_modules/vue
		cd node_modules/vue
		npm install
		npm run build

4. 使用npm搭建vue项目
		npm install -g vue-cli
		vue init webpack vue_demo
		cd vue_demo
		npm install
		npm run dev
		访问: http://localhost:8080/
```

## vue的打包与发布
```
发布 1: 使用静态服务器工具包
		npm install -g serve
		serve dist
		访问: http://localhost:5000

发布 2: 使用动态 web 服务器(tomcat)
	修改配置: webpack.prod.conf.js
		output: {
			publicPath: '/xxx/' //打包文件夹的名称
		}
	重新打包:
		npm run build
		修改 dist 文件夹为项目名称: xxx
		将 xxx 拷贝到运行的 tomcat 的 webapps 目录下
		访问: http://localhost:8080/xxx
```

## Vue实例对象的配置选项
### el
```
指定dom标签容器的选择器
Vue就会管理对应的标签及其子标签
```

### data
```
对象或函数类型
指定初始化状态属性数据的对象
vm也会自动拥有data中所有属性
页面中可以直接访问使用
数据代理: 由vm对象来代理对data中所有属性的操作(读/写)
```

### methods
```
包含多个方法的对象
供页面中的事件指令来绑定回调
回调函数默认有event参数, 但也可以指定自己的参数
所有的方法由vue对象来调用, 访问data中的属性直接使用this.xxx
```

### computed
```
包含多个方法的对象
对状态属性进行计算返回一个新的数据, 供页面获取显示
（当页面显示数据需要计算后然后再显示在页面就会用到，比如过滤后的数据）
一般情况下是相当于是一个只读的属性
利用set/get方法来实现属性数据的计算读取, 同时监视属性数据的变化
如何给对象定义get/set属性
	在创建对象时指定 : get name () {return xxx} / set name (value) {}
	对象创建之后指定: Object.defineProperty(obj, age, {get(){}, set(value){}})

```

### watch
```
包含多个属性监视的对象
分为一般监视和深度监视
	'xxx' : {
		deep : true,
		handler : fun(value)
	}
另一种添加监视方式: vm.$watch('xxx', funn)

```

## vue内置指令

### v-text/v-html: 指定标签体
```
v-text : 当作纯文本
v-html : 将value作为html标签来解析
```

### v-if v-else v-show: 显示/隐藏元素
```
v-if : 如果vlaue为true, 当前标签会输出在页面中
v-else : 与v-if一起使用, 如果value为false, 将当前标签输出到页面中
v-show: 就会在标签中添加display样式,
				如果vlaue为true, display=block, 否则是none
				如果需要频繁切换 v-show 较好
```

### v-for : 遍历
```
遍历数组 : v-for="(person, index) in persons"
遍历对象 : v-for="value in person"   $key

vue重写了数组中一系列改变数组内部数据的方法（调用原生，更新界面）
push()向数组的末尾添加一个或多个元素
pop()删除数组的最后一个元素
shift()删除数组的第一个元素
unshift()向数组开头添加一个或多个元素
splice(index, 1, val);可以实现增删改
	无论何时，使用该方法删除元素时注意数组长度有变化，bug可能就是因为它
	splice(index,1) // 删除一个元素
	splice(index,0) // 增加一个元素
	splice(index, 1, val) // 修改一个元素
sort()
reverse()
```

### v-on : 绑定事件监听
```
v-on:事件名, 可以缩写为: @事件名
// 事件绑定如果已传参数，如果需要event,需要传入$event,如：@click='click('abc',$event)'

监视具体的按键: @keyup.keyCode   @keyup.enter
	// 得到某个具体按键的keyCode值：
		<input type="text" @keydown="keydownCode">
		keydownCode (event) {
			alert(event.keyCode)
		}


停止事件的冒泡和阻止事件默认行为: @click.stop   @click.prevent
// js停止事件的冒泡和阻止事件默认行为:stopPropagation() preventDefault()

隐含对象: $event
```

### v-bind : 强制绑定解析表达式
```
html标签属性是不支持表达式的, 就可以使用v-bind
	可以缩写为:  :id='name'
:class
	:class="a"
	:class="{classA : isA, classB : isB}"
	:class="[classA, classB]"
:style
	:style="{color : color}"
```

### v-model
```
双向数据绑定
自动收集用户输入数据
常用于表单数据的搜集
```

### ref : 标识某个标签
```
ref='xxx'
读取得到标签对象: this.$refs.xxx
```

## 过渡动画
```
利用vue去操控css的transition/animation动画
模板: 使用<transition name='xxx'>包含带动画的标签
css样式
	.fade-enter-active: 进入过程, 指定进入的transition
	.fade-leave-active: 离开过程, 指定离开的transition
	.xxx-enter, .xxx-leave-to: 指定隐藏的样式

// 编码例子
<transition name="xxx">
	<p v-if="show">hello</p>
</transition>

.xxx-enter-active, .xxx-leave-active {
	transition: opacity .5s
}
.xxx-enter, .xxx-leave-to {
	opacity: 0
}
```

## vue生命周期
```
1. vue对象的生命周期
  1). 初始化显示
    * beforeCreate()
    * created()
    * beforeMount()
    * mounted()
  2). 更新状态
    * beforeUpdate()
    * updated()
  3). 销毁vue实例: vm.$destory()
    * beforeDestory()
    * destoryed()
2. 常用的生命周期方法
  created()/mounted(): 发送ajax请求, 启动定时器等异步任务
  beforeDestory(): 做收尾工作, 如: 清除定时器
```

## 自定义过滤器
```
理解
	对需要显示的数据进行格式化后再显示,如时间数据
	注意: 并没有改变原本的数据, 可是产生新的对应的数据
编码
	1). 定义过滤器
		Vue.filter(filterName, function(value[,arg1,arg2,...]){
		  // 进行一定的数据处理
		  return newValue
		})
	2). 使用过滤器
		<div>{{myData | filterName}}</div>
		<div>{{myData | filterName(arg)}}</div>

// 实例
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>11_过滤器</title>
</head>
<body>
<!--需求: 对当前时间进行指定格式显示-->
<div id="test">
  <h2>显示格式化的日期时间</h2>
  <p>{{time}}</p>
  <p>最完整的: {{time | dateString}}</p>
  <p>年月日: {{time | dateString('YYYY-MM-DD')}}</p>
</div>

<script type="text/javascript" src="../js/vue.js"></script>
<script type="text/javascript" src="https://cdn.bootcss.com/moment.js/2.22.1/moment.js"></script>
<script>
  // 定义过滤器
  Vue.filter('dateString', function (value, format='YYYY-MM-DD HH:mm:ss') {
    return moment(value).format(format);
  })

  new Vue({
    el: '#test',
    data: {
      time: new Date()
    },
    mounted () {
      setInterval(() => {
        this.time = new Date()
      }, 1000)
    }
  })
</script>
</body>
</html>
```

## 自定义指令
```
1). 注册全局指令
	Vue.directive('my-directive', function(el, binding){
		el.innerHTML = binding.value.toUpperCase()
	})

2). 注册局部指令
	directives : {
		'my-directive' : function(el, binding) {
				el.innerHTML = binding.value.toUpperCase()
		}
	}

3). 使用指令
	<div v-my-directive='xxx'>
```


