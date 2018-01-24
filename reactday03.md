	复习
	4.事件监听
	- 绑定事件监听
		- 事件名
		- 回掉函数
		- 给谁绑定
	- 触发事件
		- 用户对应的界面做对应的操作
		- 编码

	2.4 组件的组合使用
	- 1.拆分组件
	- 2.实现静态组件
	- 3.实现动态组件
		- 动态显示初始化数据
		- 交互功能(从绑定事件监听开始)


	2.5 组件收集表单数据
	- 受控组件(建议)
	- 非受控组件

	2.6 组件的生命周期
	- 1.组件的三个生命周期状态：
		- Mount：插入真实DOM
		- Update：被重新渲染
		- Unmount：被移出真实DOM

	- 2.生命周期流程
		- 第一次初始化显示
		- 每次更新
		- 删除组件

	- 3.常用方法
		- render()
		- ...

	- 虚拟DOM --> 简单的js对象(属性很少，很轻)

	- 命令式编程与声明式编程
	- 声明式编程
		- 只关注做什么，不关注怎么做(流程)
		- 类似于填空题
	- 命令式编程
		- 要关注做什么和怎么做(流程)
		- 类似于问答题

	声明式编程是建立在命令式编程的基础上

----------
	react应用(基于react脚手架)
	- 使用create-react-app
		- 这个库是帮助生成模板项目
	- xxx脚手架：用来帮助程序员快速创建一个基于xxx库的模板项目
		- 包含了所有需要的配置
		- 指定好了所有的依赖
		- 可以直接安装/编译/运行一个简单效果
	- 使用脚手架开发项目的特点：
		- 模块化、组件化、工程化

----------
	创建项目并启动
	- 全局下载
		- npm root -g 查看根目录
	- create-react-app 名字
	- cd 名字 进入
	- npm start = npm run start 
		- --> package.json中的start

	- 开发依赖 devDependencies
		- 编译打包的时候需要
		- react
		- react-dom
	- 运行依赖 dependencies
		- react-scripts

	- SPA Single Page App
		- 单页面应用

	package.json
	- 当前应用的标识文件package.json，package.json是表述当前项目的
		- 当前应用的标识
			- name --> 不变
			- version -->改变
		- 当前应用的依赖
			- dependencies 运行依赖
			- devDependencies 开发依赖
		- 运行/打包

	README.md
		- 应用的说明文件
		- 一旦提交到gitup上README就会显示


----------
	- 入口js-index.js
	- 所有的组件放在一个文件夹里components
		- 所有的组件文件名都是小写.jsx
			- app.jsx(推荐) ，也可以app.js
				- 但是组件是大写开头



----------
	app.jsx
	- import React,{Component} from 'react'
	- import logo from '../logo.svg'
	- export default class App extends Component{
		- render (){
			- return (
				- <div>
					- <img className='logo' src={logo} alt="logo">
					- <p className='title'> react app组件 </p>
				- </div>
			- )
		- }
	- }


	index.js
	- import React from 'react' --引入三方的写文件名
	- import ReactDOM from 'react-dom'
	- import App from './components/app'
	- import './index.css' --引入自定义模块必须写路径 以.或..开头

	- ReactDOM.render(<App />,document.getElementById('root'))

	- npm start 



	index.css
	- .logo{
		- width:200px
		- height:200px
	- }
	- .tltle{
		- color:red
		- font-size:25px
	- }



----------

	- 设置为模板
	- Editor--Live Templates --Template Group--xxx-Live Templates -- 内容 -- 关键字 --Define --JS，--不确定要用占位符 $className$

	- 导入配置 -代码模板
	- Import-Settings --找文件 代码模板代码样式 快捷键
	

----------
	项目
	##1.拆分组件
		- 最外围有一个组件 app组件
		- 左边组件 comment-add.jsx
		- 右边组件 comment-list.jsx
			- 列表可以拆分 comment-item.jsx

	- components文件夹
		- app文件夹--app.jsx
		- comment-add文件夹 --comment-add.jsx
		- comment-list文件夹 --comment-list.jsx
		- comment-item文件夹 --comment-item.jsx

	- 修改index里的地址

	##2.定义静态组件
	- 创建一个css文件夹，放入一个bootstrap.css
		- index里引入

	- 将index里的html拷入到app.jsx
		- class改成className
		- 要有结束符 <  />
		- style改成style={{display:'none'}}

	拆分组件
	- 左边的html拆分到comment-add.jsx中
	- 右边的拆分到conment-list.jsx中

	app.jsx中引入左右两个组件
	- import CommentAdd from '../comment-add/comment-add'
	- import CommentList from '../comment-list/comment-list'


	- <CommentAdd />
	- <CommentList />


	- comment-list文件夹下创建一个css commentList.css
	- comment-list.jsx中引入css


	- npm start


	- comment-list.jsx的14行警告此写法不好


	##3.1动态组件 --动态显示初始化数据
	- 父组件app.jsx中
	- constructor(props){
		- super(props)
		- this.state={
			- comments:[
				- {username:'Tom',content:'很好'}
				- {username:'Jack',content:'很好'}
			- ]
		- }
	- }


	- 给组建对象(this)指定state属性-->组建类
	- state = {
		- comments:[
				- {username:'Tom',content:'很好'}
				- {username:'Jack',content:'很好'}
			- ]
	- }


	- const{comments}= this.state
	- <CommentList comments={comments} />

	- 下载 npm install --sava prop-types
	- 引入PropTypes
	- CommentList.propTypes={
		- comments：PropTypes.array.isRequired
	- }

	- 在里面 给组件类添加属性
	- static propTypes = {
		- comments：PropTypes.array.isRequired
	- }

	- const {comments} = this.props

	
	- 把li给comment-item
	- 然后建一个css文件comment-item.css（拷贝list里的css）
	- 引入css
	- 引入PropTypes
	- static propTypes={
		- comment:PropTypes.object.isRequired
	- }

	- cons {comment} = this.props
	- {comment.username}
	- {comment.content}


	- 在list中引入commentItem
	- 在ul里写js代码
	- {
		- comments.map((c,index)=><CommentItem comment={c} key={index}/>)
	- }




	##3.2动态组件 --交互功能(从绑定事件监听开始)
	- 提交
	- 删除
		- 两个交互


	- 添加交互

	- add组件绑定监听
		- button onClick={this.handlesubmit}
		

		- state={
			- user:''
			- content:''
		- }

		- const {username,content} = this.state
		- value = {username} onChange={this.handleNameChange}

		- value = {content} onChange={this.handleContentChange}


		- 写自定义的方法
		- handleSubmit=()=>{
			- //收集数据,并封装成comment对象
				- 受控组件--必须有状态
				- const comment = this.state
			- //更新状态
		- }
			- 箭头函数没有自己的this。看外围的，正好是组建对象

		- handleNameChange=(event)=>{
			- const username = event.target.value
			- 
		- }

		
		- handleContentChange=()=>{
			- 
		- }
	
		- app.jsx
		- addComment = (comment)=>{
			- 
		- }
	

----------
	react ajax
	- 1.理解
	- 1.1 前置说明
		- 1，

	- 1.2 常用的ajax请求库
		- 1，jQuery比较重，如果需要另外引入不建议舒勇
		- 2，axios：轻量级，建议使用
			- a,封装XmlHttpRequest对象的ajax
			- b,promise风格
			- c,可以用在浏览器端和node服务器端
		- 3，fetch：原生函数，但老版本浏览器不支持
			- a,不再使用XmlHttpRequest对象提交ajax请i去
			- b,为了兼容低版本的浏览器，可以引入兼容库fetch.js

	

----------
	- class MostStarRepo extends React.Component{
		- state={
			- repoName:'',
			- repoUrl:''
		- }	
		 
		- componentDidMount(){
			- //使用axios发送异步的ajax请求 - 引入axios.js
			- const url = ''
			- axios.get(url).then(reponse=>{
				- const result = response.data
				- //console.log(reponse)
				- 得到数据
					- const {name,html_url} = result.items[0]
				- 更新状态
					- this.setState({repoName:name,repoUrl:html_url})
				- .catch(error)=>{
					- alert(err.message)
				- }
				
			- })
				- axios.get(url).then() -->返回的是promise对象



			- 使用fetch发送异步的ajax请求
				- fetch(url)
					- .then(response=>{
						- return response.json()
					- })
					- .then(data=>{
					- 得到数据
						- const {name,html_url} = result.items[0]
					- 更新状态
						- this.setState({repoName:name,repoUrl:html_url})
					- })


		- } 
			
		- render(){
			- const {repoName,repoUrl}=this.state
			- if(!repoName){
				- return <h2>Loading</h2>
			- }else{
				- return <h2>Most star repo is <a href={repoUrl}>{repoName}</a></h2>
			- }
		- }
	- }

	- ReactDOM.render(<MostStarRepo />,document.getElementById(''))


----------
	demo
	- app.jsx
	- search.jsx
	- main.jsx

	- indx.js
		- 引入css import

	- app.jsx
	- 把html粘贴进来 class-className
	- style={{}}


	- search.jsx
	- 把html粘贴进来

	- main.jsx
	- 把对应的html粘贴进来


	- app.jsx
	- 引入两个组件 Search Main
	- return <Search /> <Main />
	- index里修改路径

	## 3.1
	- main组件一共有四个状态
	- 初始化状态
	- state ={
		- initView：true，
		- loading：false， -->Loading的文本
		- users：null，
		- errorMsg:null -->请求出错
	- }

	- render(){
		- const{ , , , }=this.state

		- if(){
			- 
		- }else if(){
			- 
		- } else if(){
			- 
		- }else{
			- {
				- users.map((user,index)=>(
					- 此时箭头代表一个是函数，一个是返回
					- a href={user.url}
					- img src={user.avatarUrl}
					- p {user.name}
				- ))
			- }
		- }
	- }

	- 在main.jsx组件中发送请求


	- app.jsx
	- state={
		- searchName:''
	- }

	- setSearchName=(searchName)=>{
		- this.searchName = searchName
	- }
	- <Search />

	- search.jsx
	- button onClick={this.search}
	- import PropTypes
	- static propTypes={}
	- search=()=>{}
	- input ref={input=>this.input=input}
	- 得到输入的关键字
		- const searchName=this.input.value.trim()
		- if(searchName){
			- 搜索
		- }

	- app.jsx
	- <Main ../>
	


	- main.jsx
	- import PropTypes from ''
	- static propTypes={}
	- render(){
		- const{}=this.props
	- } 


	- app.jsx
	- 更新状态
	- this.setState({})


	- main.jsx
	- 当组件接收到新的属性时回掉
	- componentWillReceiveProps(）{}
	- import axios
		- npm install --save axios
	- 更新状态(请求中)
	- this.setState({})
	- 发请求ajax
	- const url=
	- axios.get(url)
	- .then()
	- .catch()
	- const users = result.items.map()
	- this.setState()

----------
	1.组件间通信
	- 1.1 方式一：
	- 1.2 方式二：使用消息订阅-发布机制
		- 添加订阅相当于绑定监听
		- 发布消息相当于触发事件
		- 1.工具库：PubSubJS