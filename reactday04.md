	- 一个组件对应一个文件夹，因为有可能包含css，jsx->js和html
	- 文件夹名用小写，comment-add


	- props
	- 父组件传递数据：父组件传递给子组件
	- 父组件向子组件传递函数，子组件有能力更新父组件的状态

	- props只能父子传递
		- 兄弟之间传递要借助父组件
	
	- 对象的简洁表达 {a,b}
		- {a=a,b=b}
	
	- ()=>{} 箭头函数本身是匿名函数
		- xxx=()=>{}给箭头函数定义名字
		- 没有自己的this，使用引用this查找的是外部this

	- 项目打包运行
	- npm run build 
		- 生成打包文件
	- npm install -g serve
		- 全局下载服务器包
	- serve build
		- 通过服务器命令运行打包项目
	- 访问
		- public里是要打包的

	

----------
	react-router4
	- 理解：
	- react的一个插件库
	- 专门用来实现一个SPA应用
	- 基于react的项目基本都会用到此库
		- -->必须有jQuery

	- SPA 单页Web应用
	- 1，单页Web应用（single page web application，SPA）
	- 2，整个应用只有一个完整的页面
	- 3，点击页面中的链接不会刷新页面，本身也不会向服务器发送请求
	- 4，当点击路由链接时，只会做页面的局部更新
	- 5，数据都需要通过ajax请求获取，并在前端异步展现


	- 单页链接 = 路由链接
	

----------
	路由的理解
	- router.get（path，function(req,res){}）
	- router.post --> 路由器

	- 路由 route   --> 一个路由就是一个映射关系
		- key-value key为路由路径，value可能是function(后台路由)/component(前台路由)
	- 路由器 router


	- 后台路由处理前台路由的请求


	2)路由分类
		a.	后台路由: node服务器端路由, value是function, 用来处理客户端提交的请求并返回一个响应数据
		b.	前台路由: 浏览器端路由, value是component, 当请求的是路由path时, 浏览器端前没有发送http请求, 但界面会更新显示对应的组件 
	3)后台路由
		a.	注册路由: router.get(path, function(req, res))
		b.	当node接收到一个请求时, 根据请求路径找到匹配的路由, 调用路由中的函数来处理请求, 返回响应数据
	4)前端路由
		a.	注册路由: <Route path="/about" component={About}>
		b.	当浏览器的hash变为#about时, 当前路由组件就会变为About组件


----------
	- react-router
	- 1，组件
		- <BrowserRouter>
		- <HashRouter>
		- <Route>
		- <Redirect>
		- <Link>
		- <NavLink>
		- <Switch>

	

----------
	- 下载npm install --save react-router-dom
	- src
		- index.js
			
		- components -->一般组件文件夹
			- app.jsx
		- views -->路由组件文件夹
			- about.jsx
			- home.jsx
	- public
			- css--bootstrap
			

----------
	index.js
	- import React from 'react'
	- import {render} from 'react-dom'
	- import {BrowserRouter} from ''
	

	- import App from './'


	- render((
		- <BrowserRouter>
		- <App />
		- </BrowserRouter>
	- ),document.getElementById(''))


	-

----------
	app.jsx
	- 引入html
	- import {NavLink,Switch,Route,Redirect} from ''
	- <NavLink className='' to='/about'>About</NavLink>
	- <NavLink className='' to='/home'>Home</NavLink>

	- import About from ''
	- import Home from ''
	- <Switch>
		- <Route path='/about' component={About}/>
		- <Route path='/home' component={Home}/>
		- <Redirect to='/about'>
	- </Switch>


	- about.jsx
	- <div></div>


	- home.jsx
	- <home></home>


----------
	- <NavLink className='' to='/about' activeClassName='activeClass'>About</NavLink>
	- <NavLink className='' to='/home' activeClassName='activeClass'>Home</NavLink>


	- 定义一个组件--代码优化 MyNavLink
	- import {NavLink} frm ''
	将外部传入的所有属性传递给NavLink
	- return <NavLink {...this.props}activeClassName='activeClass'/>


	- app.jsx
	- import MyNavLink from ''
	- <MyNavLick ...>


----------
	- Home 一级路由
		- 二级路由

	- 嵌套路由使用
	

	- 如何编写路由效果
	- 1，编写路由组件
	- 2，在父路由组件中指定两个标签
		- 路由链接:<NavLink> 
		- 路由:<Route>
		

----------
	- views
		- news.jsx
		- message.jsx

	## news.jsx
	- state = {
		- newsArr:[
			- 'sfe'
			- 'asd'
			- 'sad'
		- ]
	- }
	
	- <ul>
		- {this.state.newsArr.map}
	- </ul>





	## message.jsx
	- state = {
		- messages:[
			- {id:1,title:'message001'},
			- {},
			- {}
		- ]
	- }

	模拟发送ajax异步请求获取数据
	- componentDidMount(){
		- setTimeout(()=>{
			- const message = []
			更新状态
			- this.setState({messages})
		- },2000)
	- }

	- <ul>
		- {this.state.messages.map((m,index=>(
			- <li>
				- <a href=''>{m.title}</a>
			- </li>
		- )))}
	- </ul>


----------
	## home.jsx
	- import MyNavLink from ''
	- import {}
	- import News
	- import Messages
	
	- <div>
		- <div>
			- <ul>
				- <li>
					- <MyNavLinK to=''></MyNavLinK>
					- <MyNavLinK to=''></MyNavLinK>
				- </li>
			- </ul>
			- <div>
				- <Switch>
					- <Route path='' component={}>
					- <Route path='' component={}>
					- <Redirect to=>
				- </Switch>
			- </div>
		- </div>
	- </div>


----------
	向路由组件传递参数数据
	- message-detail.jsx
	- import React from ''

	- const allMessages=[
		- {}
	- ]

	-  <ul>
		- <li>ID:??</li>
		- <li>TITLE:??</li>
		- <li>CONTENT:???</li>
	-  </ul>


	message.jsx
	- import {Route} from
	- import MessageDetail

	- <div>
	- <ul>
		- {this.state.messages.map((m,index=>(
			- <li key>
				- <a href={}>{m.title}</a>
			- </li>
		- )))}
	- </ul>
	- <Route path='/:id(即是占位符也是标识名称)' component={MessageDetail}/>
	- </div>


	- message-detail.jsx
	得到请求参数中的id
		- const {id}=props.match.params
	查询得到对应的message
		- const message = allMessages.find()
	-  <ul>
		- <li>ID:{message.id}</li>
		- <li>TITLE:{message.title}</li>
		- <li>CONTENT:{message.content}</li>
	-  </ul>

----------
	message.jsx
	- shouDetail=(id)=>{
		- this.props.history.push()
	- }
	- shouDetail2=(id)=>{
		- this.props.history.push()
	- }
	- back=()=>{}
	- forword=()=>{}

	- <ul>
		- {this.state.messages.map((m,index=>(
			- <li key>
				- <MyNavLink></>
				- <button onClick={()=>{this.showDetail(m.id)}}>
				- <button onClick={()=>{this.showDetail2(m.id)}}>
			- </li>
		- )))}
	- </ul>
	- <p>
		- <button onClick={this.back
		- <button onClick={this.forward
	- </p>

	- 页面跳转
	- window.location=''


----------
	- 定义路由组件
	- <Link>
	- <Route>
	- 

----------
	- material-UI

	- ant-design
	

----------
	- index.jsx
	- component
		- app.jsx


----------
	index.js
	- import 。。
	- render()


----------
	app.jsx
	- improt
	- npm install antd-mobile --sava下载
	- <Button>Start</>


	index.html
	- 引入script


----------
	- 按需打包--强烈推荐
	- babel-plugin-import(推荐)
		- 只加载import执行的模块
	

----------
	- 下载依赖包
		- npm ....
	- 修改默认配置 package.json


----------
	- 在你开始项目前，你需要决定你使用的路由器的类型。对于网页项目，存在<BrowserRouter>与<HashRouter>两种组件。当存在服务区来管理动态请求时，需要使用<BrowserRouter>组件，而<HashRouter>被用于静态网站。
	
	- 通常，我们更倾向选择<BrowserRouter>，但如果你的网站仅用来呈现静态文件，那么<HashRouter>将会是一个好选择。


