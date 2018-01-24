	React全家桶(技术栈)
	- React基本认识
		- 用于构建用户界面的JavaScript库
		- 构建用户界面：把数据展现出来

	特点
	- 声明式
	- 组件化
	- 一次学习，随处编写
	- 高效
	- 单项数据流

	高效的原因
	- 虚拟DOM，不总是直接操作DOM 
		- 虚拟DOM --> 对象，与DOM对应
		- 然后修改虚拟DOM，最后映射到DOM上-->批量修改
	- DOM Diff算法，最小化页面重绘
		- 算哪些地方需要变 -->减少更新的区域

----------
	React的基本使用
	- BootCDN --> 下载库
		- react.js --> React核心库
		- react-dom.js -->提供操作DOM的react扩展库
		- babel.min.js -->解析JSX语法代码转为纯JS语法代码的库

	- test.html
	- 引入三个js文件
	- div id#test
	- script type="text/babel" -->告诉babel.js解析jsx的代码
	1，创建虚拟DOM元素对象
	- var vDom = <h1> Hello</h1> //不是字符串
	2，将虚拟DOM渲染到页面真实DOM容器中
	- ReactDOM.render(vDom,document.getELementById('test'))

	使用React开发者工具调试

----------
	JSX
	- div#test1
	- div#test2
	script
	- const msg = 'I Like You'
	- const myId = 'Atguigu' 
	- 1，创建虚拟DOM
		- const vDom = React.creatElement('标签名',{标签属性},值) 
		- const vDom = React.creatElement('h2',{id:myId.toLowerCase()},msg.toUpperCase())
		- const test1Div = document.getElementById('test1') -->真实DOM，比较重，而且会更新界面
		- debugger --> 断点
	- 2，渲染虚拟DOM -->渲染的时候才会更新DOM
		- ReactDOM.render(vDom1,document.getELementById('test1'))

	方式二
	script type="text/babel"
	- 1，创建虚拟DOM
		- const vDOm2 = <h3 id={myId.toUpperCase()}>{msg.toLowerCase()}</h3>
			- {} -->表示内部是变化的值
	- 2，渲染虚拟DOM
		- ReactDOM.render(vDom1,document.getELementById('test1'))
	

----------
	- 虚拟DOM最终都会被转换成真实的DOMh3，虚拟DOM中的h3与真实DOM中的h3是对应关系


----------
	JSX - JavaScript XML 
	- 可以自定义标签名 --组建标签

	- react定义的以中类似于XML的JS扩展语法:XML+JS
	- 标签名任意
	- 标签属性任意
	- 基本语法规则
		- 1，
		- 2，
	- babel.js的作用


	渲染虚拟DOM
	- 语法
	- 创建虚拟DOM的2种方式
		- 1，
		- 2，
	

----------
	练习
	- 问题：如何将一个数据的数组转换为一个标签的数组
		- 使用数组的map()方法

	- div#example1
	- const names = ['jQuery', 'zepto', 'angular', 'react', 'vue']
	- 1,创建虚拟DOM
		- //<ul><li>{name}</li></ul>
		- const ul = (
		<ul>
			{
			names.map((name,index)=><li key="{index}">{name}</li>)
			}
		</ul>
		)
	- 2，渲染虚拟DOM
	- ReactDOM.render(ul,getElementById('example1'))


	