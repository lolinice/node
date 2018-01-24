	模块与组件和模块化与组件化的理解
	- 模块：
		- 向外提供特定功能的js程序，一般就是一个js文件
		- 一个有特定功能的js文件
		- ...没听见
	- 模块化：
		- 形容项目，写js的时候是一个模块一个模块编写的
	- 组件
		- 用来实现特定(局部)功能效果的代码集合
		- 编写组建涉及到html,css,js
	- 组件化：
		- 形容编写方式

	- 一般是组件化编写的前提都是模块化，反之不一定

----------
	React面向组件编程
	- js是面向对象编程，
		- 面向对象-->面向模块-->面向组件

	- 组件标签 -->首字母大写，区别html标签

	- 1，定义组件
		- 方式1：工程函数组件(简单组件)
		- function MyComponent(){
			- returen <h2>工厂函数组件(简单组件)</h2>
		- }


		- 方式2：ES6类组件(复杂组件)
		- class MyComponent2 extends React.Component{
			- render(){
				- conso(this)
				- return <h2></h2>
			- }
		- }
			- 创建实例,调用render方法	
			- MyComponent2 组件类
			- this指向组件实例对象	


	- 2，渲染组件标签
	- ReactDOM.render(<MyComponent />,document.getElementById('example1'))
		- 渲染MyComponent标签的时候，会调用组件
	- ReactDOM.render(<MyComponent2 />,document.getElementById('example2'))

----------
	组件的三大属性
	- 1.state
		- state是组件对象最重要的属性，值是对象(可以包含多个)
	- 编写操作
		- 初始化状态
		- 读取某个状态值
		- 更新状态-->组件界面更新
			- this.setState()
				## this-->组件对象


	- 1，定义组件
		- 定义类名为Like 继承 React的Component属性
	- class Like extends React.Component{
		- constructor(props){
			- super(props)
				- 调用父类型的构造函数，把props传给它
			1，初始化状态
			- this.state={
				- isLikeMe:false
			- }
		## 将新增方法中的this强制绑定为组件对象
			- this.handClick = this.handleClick.bind(this)
				- .bind产生一个新的函数，新的函数指定的this
			
		- }


	## 新添加方法：内部的this默认不是组件对象，而是undefined
		- handleClick(){
			- 得到状态,并取反
			- const isLikeMe = ！this.state.isLikeMe
			3，更新状态
			- this.setState({isLikeMe})
		- }


	 重写组件类的方法，本就有render方法 -->render 方法，用于输出组件。
		- render(){
			2，读取状态
			const {isLikeMe} = this.state
			- return <h2 onClick={this.handleClick}>{isLikeMe?'你喜欢我':'我喜欢你'}</h2>
		- }
	- }


	- 2，渲染组件标签
	- ReactDOM.render(<Like />,document.getElementById('example'))


----------
	- 组件如果有状态就不能用工厂模式
		- 简单组件:没有状态的组件

----------
	- 1，定义组建
	没有状态，接收的是属性-->工厂函数方式
	- function Person(props){
		- return(
			- <ul>
				- <li>姓名：{props.name}</li>
				- <li>年龄：{props.age}</li>
				- <li>性别：{props.sex}</li>
			- </ul>
		- )
	- }

	指定属性默认值
	- Person.defaultProps = {
		- sex:'男'
		- age:18
	- }
	

	## 对props中的属性值进行类型限制和必要性限制
		- 下载对应的库
		- 然后引入进来prop-types

	指定属性值的类型和必要性
		- Person.propTypes = {
			- name:PropTypes.string.isRequired,
			- age:PropTypes.number
		- }


	- 2，渲染组件标签
	- const p1 = {
		- name:'Tom'
		- age:18
		- sex:'女'
	- }
	- ReactDOM.render(<Person name={p1.name} age={p1.age} sex={p1.sex}"/>,document.getElementById('example1'))

	- ReactDOM.render(<Person {...p1}/>,document.getElementById('example1'))
	
	### ...的作用
	- 1，打包
		- function fn(...as){}
		- fn(1,2,3)
			- as是个数组，把123打包
	- 2，解包 -->将一个数组或对象中的东西拿出来
		- const arr1 = [1,2,3]
		- const arr2 = [6,...arr1,9]


	- const p1 = {
		- name:'Tom'
		
	- }
	- ReactDOM.render(<Person name={p2.name} age={20} />,document.getElementById('example2'))

	## 语法糖 -->简洁语法


	- Class Person extends React.Component {
		- render(){
			- return(
			- <ul>
			this是组建对象Props
				- <li>姓名：{this.props.name}</li>
				- <li>年龄：{this.props.age}</li>
				- <li>性别：{this.props.sex}</li>
			- </ul>
			- )
		- }
	- }


----------
	- 1,定义组件
	- Class MyComponent extends React.Component{
		- constructor(props){
			- super(props)
			- this.showInput = this.showInput.bind(this)
		- }

		- showInput(){
		## ref作用: 通过ref获取组件内容特定标签对象, 进行读取其相关数据
			- const input = this.refs.content
			- alert(input.value)
			- alert(this.input.value)
		- }

		- handleBluer(event){
			- alert(event.target.value)
				//event.target --> input
		- }


		- render(){
			- return(
				- <div>
					- <input type="text" ref="content" />
	
					- <input type="text" ref={input=>this.input=input} />
						- ref等于一个回掉函数，input是当前inputDOM元素，this是组建对象，绑定到了组件对象上的input
	
					- <button onClick={this.showInput}>提示输入</button>
					- <input type="text" placeholder="失去焦点提示功能" onBlur={this.handleBlur}/>
				- </div>
			- )
		- }
	- }



	- 2，渲染组件标签
	- ReactDOM.render(<MyComponent />,document.getElemntById('example'))

	##做交互从绑定事件监听开始


----------
	组件的组合
	## 功能界面组件化编码流程
	- 拆分组件
		- 跟组件 APP
		- 上半部分-->添加组件 Add
		- 下半部分-->列表组件 List
	- 实现静态组件：使用组建实现静态页面效果
	- 实现动态组件
		- 1，动态显示初始化数据
		- 2，交互功能(从绑定事件监听开始)


	- 一个组件组件只能有一个根标签

	## 数据保存在哪个组件内?
	- 看数据是某个组件需要(给他)，还是某些组件需要(给共同的父组件)

	## 需要在子组件中改变父组件的状态
	- 子组件中不能直接改变父组件的状态
	- 状态在哪个组件，更新状态的行为就应该定义在哪个组件
		- 行为-->函数或者方法
	- 解决：父组件定义函数，传递给子组件，子组件调用

----------
	- class App extends React.COmponent{

		- constructor(props){
			- super(props)
			- this.state = {
				- todo:['吃饭','睡觉','打游戏']
			- }
			- this.addTodo = this.addTodo.bind(this)
		- }

		- addTo(todo){
			- const {todo}= this.state
			- todos.unshif(todo)
			- this.setState({todos})
		- }



		- render (){
			- const {todos}= this.state
			- return(
				- <div>
					- <h1> Simple TODO List</h1>
					- <Add count={todos.length} addTodo={this.addTodo}/>
					- <List todo={this.state.todo}/>
				- </div>
			- )
		- }
	- }


	- class Add extends React.COmponent{
	
	- constructor(props){
			- super(props)
			- this.add = this.add.bind(add)
			- }
		- }
		## 只要是自己定义的方法，一般都要绑定this

		- add(){
			- 1,读取输入的数据
				- const todo = this.todoInput.value.trim()
			- 2，检查合法性
				- if(!todo){
					- return
				- }
			- 3，添加
				- this.props.addTodo(todo)

			- 4，清除输入
				- this.value = null
			
		- }


		- render (){
			- <input type="text" ref={this.todoInput=input}/>
			- <button onClick={this.add}>#{this.props.count+1}</button>
		- }
	- }


	- Add.propTypes = {
		- count:PropTypes.number.isRequired
		- addTodo:PropTypes.func.isRequired
	- }



	- class List extends React.COmponent{
		- render (){
			- <ul>
				- {
					- this.props.todos.map((todo,index)=><li key=index>{todo}</li>)
				- }
			- </ul>
		- }
	- }

	- List.propTypes = {
		- todo:PropTypes.array.isRequired
	- }


	- ReactDOM.render(<APP />,document.getElemntById('example'))


----------
	流程：
	- 1.拆分组件
	- 2.实现静态组件 --> 只有静态页面，没有动态数据和交互
		- render(){
			- return 
		- }

	- 3.实现动态组件
		- 1，实现初始化数据动态显示
			- 思考：数据保存在哪个组件
		- 2，实现交互功能
			- 绑定事件监听

----------
	收集表单数据
	- class LoginForm extends React.Component{
		//2
		constructor(props){
			super(props)
			this.handleSubmit=this.handleSubmit.bind(this)
			this.handleChange=this.handleChange.bind(this)

			//6
			this.state={
				this.state={
					pwd:""
				}
			}		

		}

		
		handleSubmit(event){
			//5
			const name = this.nameInput.valye
			//8
			const {pwd} = this.state
			alert(${name},${pwd})

			//3.阻止默认行为
			event.preventDefault()
			
			//7.'
			handleChange(event){
				//读取输入的值
				const.pwd = event.target.value
				//更新pwd的状态
				this.setState({pwd})
			}

		}


		//1.
		- render(){
			- return(
				- <form action="/test" 1.onSubmit={this.handleSubmit}>
					- 用户名：<input type="text" 4ref={input=>nameInput=input}>
					- 密码:<input type="password" value={this.state.pwd} onChange={this.handleChange}>
					- <input type="submit" value="登陆">
				- </form>
			- )
		- }
	- }

	- ReactDOM.render(<LoginForm/>,document.getElementById('example'))


----------
	包含表单的组件分类
	- 受控组件：表单输入数据能自动收集成状态（推荐）
	- 非受控组件：

----------
	组件生命周期
	- 1.class Life extend
		- 9.constructor
			- 10.super
			- 11.this.state ={
				- opcity:1
			- }
			- 21.this = 

		- 20 dis（）{
			- 22.ReactDOM
		- }

		- 12.componentDidMount(){
			- 放在同一个对象里 都能看见定时器
			- this.intervalId = setInterval(function(){ //不是这个函数，是通过this产生的新的函数
				- 13.let{}
				- //18. -=
				- 14.opcity
				- 15.if(){
					- 16.
				- }
				- 17.this.setState({opacity})
			- }.bind(this(此时的this是这个方法里的this，因为定时器里的this是window)),200)
		- }


		- 23.componentWillUnmount(){
			- 清理定时器
			- 24.clearInter(this.intervalId)
		- }		

	
		- 2.render(){
			- 12.const{opacity} = this.state
			- 3.return(
				- 4.div
					- 5.<h2 8.style=13{外面大括号代表里面是js代码{里面的大括号代表我是一个js对象}} {6.}>
					- 7.<button 19.onClick={this.dis...}>
			- )
		- }


	- 4.ReactDOM.render(<Life 6.msg="">)


	- 构造器
	- 只要状态变了就要调用render()方法
	- DidMount 执行一次 初始化
	- WillMount 执行一次 死亡



----------
	虚拟DOM与DOM Diff算法
	- 