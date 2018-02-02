	redux
	- redux是一个独立专门用于做状态管理的JS库（不是react插件库）
	- 它可以在react,angular,vue等项目中，但基本与react配合使用
	- 作用：集中式管理react应用中多个组件共享的状态
		- 集中式管理 App 


----------

	- increment ()=>{
		- //1.得到选择增加的数量
		- const number = this.select.value*1
		- //2.得到原本的count状态，并计算新的count
		- const count= number + this.state.count
		- //3.更新状态
		- this.setState({count})
	- }

	- IncrementIfOdd ()=>{
		- //1.得到选择增加的数量
		- const number = this.select.value*1
		- //2.得到原本的count状态，并计算新的count
		- const count= number + this.state.count
		
		- 判断，满足条件才更新状态
		- if(count%2=1){
			- //3.更新状态
			- this.setState({count:count+number})
		- }
	- }


----------
	- 获取状态显示 getState
	- 分发 dispatch(action) -->调用lintener回掉函数
	- 订阅 subsctibe(listener)
	

	- action就是更新的行为

----------
	2.2. store对象
	1)	作用: 
	redux库最核心的管理对象
	2)	它内部维护着:
			state
			reducer
	3)	核心方法:
			getState()
			dispatch(action)
			subscribe(listener)
	4)	编码:
			store.getState()
			store.dispatch({type:'INCREMENT', number})
			store.subscribe(render)
	
	
	2.3. applyMiddleware()
	1)	作用:
	应用上基于redux的中间件(插件库)
	2)	编码:
	import {createStore, applyMiddleware} from 'redux'
	import thunk from 'redux-thunk'  // redux异步中间件
	const store = createStore(
	  counter,
	  applyMiddleware(thunk) // 应用上异步中间件
	)
	
	
	2.4. combineReducers()
	1)	作用:
	合并多个reducer函数
	2)	编码:
	export default combineReducers({
	  user,
	  chatUser,
	  chat
	})



----------

3. redux的三个核心概念

	3.1. action
	标识要执行行为的对象
	包含2个方面的属性
		type: 标识属性, 值为字符串, 唯一, 必要属性
		xxx: 数据属性, 值类型任意, 可选属性
	例子:
		const action = {
			type: 'INCREMENT',
			data: 2
		}
	Action Creator(创建Action的工厂函数)
		const increment = (number) => ({type: 'INCREMENT', data:number})
		- {}返回的是一个对象，不加()否则{}就不会作为对象的标识，而是作为函数体的标识


3.2. reducer
	根据老的state和action, 产生新的state的纯函数
	样例
		export default function counter(state = 0, action) {
		  switch (action.type) {
		    case 'INCREMENT':
		      return state + action.number 新状态
		    case 'DECREMENT':
		      return state - action.number
		    default:
		      return state
		  }
		}
	注意
		返回一个新的状态
		不要修改原来的状态


3.3. store
	将state,action与reducer联系在一起的对象
	如何得到此对象?
		import {createStore} from 'redux'
		import reducer from './reducers'
		const store = createStore(reducer)
	此对象的功能?
		getState(): 得到state
		dispatch(action): 分发action, 触发reducer调用, 产生新的state
		subscribe(listener): 注册监听, 当产生了新的state时, 自动调用


	实际应用中，Reducer 函数不用像上面这样手动调用，store.dispatch方法会触发 Reducer 的自动执行。为此，Store 需要知道 Reducer 函数，做法就是在生成 Store 的时候，将 Reducer 传入createStore方法。
	
	import { createStore } from 'redux';
	const store = createStore(reducer);
	上面代码中，createStore接受 Reducer 作为参数，生成一个新的 Store。以后每当store.dispatch发送过来一个新的 Action，就会自动调用 Reducer，得到新的 State。

----------
	## store.js

	import {createStore} from 'redux'
	import {counter} from ''
	- 生成一个store对象
	- const store = createStore(counter)
		- 内部会第一次调用reduer函数，得到初始state







----------
	- 安装稳定版：

		npm install --save redux


----------
	## reducers.js
	- import {InCREMENT,DECREMENT} from ''
	
	包含多个reducer函数的模块 reducers.js
	
	- export function counter(state=0,action){
		- switch(action.type){
			- case "INCREMENT":
				- return state + action.data
			- case "ENCREMENT":
				- return state - action.data
			- default: 
				- return state
		- }
	- }




----------
	- action-typres.js
		- 包含
	- export const InCREMENT = 'InCREMENT'
	- export const DECREMENT = 'DECREMENT'


----------
	react-redux
	- react插件库
	- 专门用来简化react应用中使用redux
	

----------
	## 1.改造从index.js开始
	- import {Provider} from ''
	- <Provider store={store}>
		- <App/>
	- </>

	## 重点变化在组件里
	
	- import {connect} from '' 
		- 链接react组件和redux
		- connect 是个函数

	- 声明propTypes
	- static propTypes={
		- count:PropTypes.number.isRequired,
		- increment:PropTypes.func.isRequired,
		- decrement:PropTypes.func.isRequired
	- }

	- const ...
	- increment ()=>{
		- //1.得到选择增加的数量
		- const number = this.select.value*1
		- this.props.increment(number)
		
	- }

	- export default connect(
		- state=>({count:state}),//函数返回值是一个对象，state是redux里管理的state，就是
		- {increment,decrement}
	- )(App)

	- {count：}和{increment(app的属性名，必须和声明的属性名一样)：increment（和action声明的属性名一样），de}解构赋值放到App组件里
	- 包装App给其传数据，


----------
	5.2. React-Redux将所有组件分成两大类
	1)	UI组件
	只负责 UI 的呈现，不带有任何业务逻辑
	通过props接收数据(一般数据和函数)
	不使用任何 Redux 的 API
	一般保存在components文件夹下
	
	2)	容器组件
	负责管理数据和业务逻辑，不负责UI的呈现
	使用 Redux 的 API
	一般保存在containers文件夹下


----------
	- 问题：
	- 1，redux默认是不能进行异步处理的
	## 解决——下载redux插件(异步中间件)
	
	- 6.1. 下载redux插件(异步中间件)
	npm install --save redux-thunk
	
	## 6.2. index.js
	import {createStore, applyMiddleware应用一个中间件} from 'redux'
	import thunk from 'redux-thunk'
	// 根据counter函数创建store对象
	const store = createStore(
	  counter,
	  applyMiddleware(thunk) // 应用上异步中间件
	)
	
	
	## 6.3. redux/actions.js
	//同步的action都返回一个对象
	// 异步action creator(返回一个函数)
	export const incrementAsync = number => {
	  return dispatch => {
		## 在函数中才能执行异步代码
	    setTimeout(() => {
			##1s后才能去分发一个增加的action
	      dispatch(increment(number))
	    }, 1000)
	  }
	}
	- return返回一个函数，靠异步中间件来调
	
	
	## 6.4. components/counter.jsx
	incrementAsync = () => {
	  const number = this.refs.numSelect.value*1
	  this.props.incrementAsync(number)
	}
	
	## 6.4. containers/app.jsx
	import {increment, decrement, incrementAsync} from '../redux/actions'
	// 向外暴露连接App组件的包装组件
	export default connect(
	  state => ({count: state}),
	  {increment, decrement, incrementAsync}
	)(Counter)

----------
	7. 使用上redux调试工具
	
	## 7.1. 安装chrome浏览器插件
	 
	## 7.2. 下载工具依赖包
	npm install --save-dev redux-devtools-extension
	## 7.3. 编码
	import { composeWithDevTools } from 'redux-devtools-extension'
	
	const store = createStore(
	  counter,
	  composeWithDevTools(applyMiddleware(thunk)) 
	)
	
	
	##　8. 相关重要知识: 纯函数和高阶函数
	## 8.1. 纯函数
	1)	一类特别的函数: 只要是同样的输入，必定得到同样的输出
	2)	必须遵守以下一些约束  
	不得改写参数
	不能调用系统 I/O 的API
	不能调用Date.now()或者Math.random()等不纯的方法  
	3)	reducer函数必须是一个纯函数
	
	## 8.2. 高阶函数
	1)	理解: 一类特别的函数
	参数是函数
	返回是函数
	2)		常见的高阶函数: 
			数组的map()/filter()/reduce()/find()
			ajax请求函数
			定时器设置函数
			react-redux中的connect函数
	3)		作用: 
			能实现更加动态, 更加可扩展的功能


----------
	- comments:[] 开始是一个空数组
	- 在componentDidMount发请求
		- 模拟发送异步ajax请求，获取数据
		- setTimeout(()=>{})

	
----------
	## UI组件 components文件夹下
	只负责 UI 的呈现，不带有任何业务逻辑
	通过props接收数据(一般数据和函数)
	不使用任何 Redux 的 API
	一般保存在components文件夹下
	
	## 容器组件 containers文件夹下
	负责管理数据和业务逻辑，不负责UI的呈现
	使用 Redux 的 API
	一般保存在containers文件夹下

	## redux里
	- action-types.js 包含所有action的type名称常量
	- action.js 包含了所有的action creator(action的工厂函数)
	- reducers.js 包含n个reducer函数(根据老的state和action返回一个新的state)
	- store.js redux最核心的管理对象store

	## components文件夹下
	- app.js


----------

	- index.js中
	- import {Provider}
	- import store
	- import App
	- <Provider>
		- <App/>
	- </Provider>	
	- 

----------
	app.jsx
	- import {PropTypes}
	- import {connect}
	- import {add，delete}
	- static propTypes ={
		- comments:
		- addComment:
		- deleteComment:
	- }

	- const {comments,addcomment,deletecomment}=this.prop
	- export default connect(state=>({comments:state})
	- {add。。,delete。。}
	- (App) //state就是一个comments数据


----------
	action-types
	## 添加评论
	- export const ADD_COMMENT='add_comment'
	## 删除评论
	- export const DELETE_COMMENT='delete_comment'


----------
	action.js
	- import {ADD_COMMENT,DELETE_COMMENT}
	## 同步添加
	- export const addComment=(comment)=>({
		- type:ADD_COMMENT,
		- data:comment
	- })

	## 同步删除
	- export const deleteComment=(comment)=>({
		- type:DELETE_COMMENT,
		- data:index
	- })

----------
	reducers.js
	- import {ADD_COMMENT,DELETE_COMMENT}
	- const initComments = [
		- {}
	- ]
	- exports function comments(state=initComments,action){
		- switch (action.type){
			- case ADD_COMMENT:
				- return [action.data,...state]
			- case DELETE_COMMENT:
				- return state.filter((comment,index=>index!==action.data))
					- 过滤，产生一个新的数组，不改变原数组
			- default:
				- return state
		- }
	- }


----------
	store.js
	- import {createStore,applyMiddleware} from ''
	- import {comments} from ''
	- import thunk from ''
	- import {composeWithDevTools}

	- export default createStore(
		- comments,
		- composeWithDevTools(applyMiddleware(thunk))
	- )
	

----------
	reducers.js
	- const initComments = []


----------
	action.js
	- 同步接收 comments
	- const receiveComments =(comments)=>({type:Receive_Comments,data:comments})


	- 异步从后台获取数据
	- export const getComments = ()=>{
		- return dispatch = >{
			- 模拟发送ajax请求异步获取数据
			- setTimeout (()=>{


			分发一个同步的action
			dispatch(receiveComments(comments))
			- },1000)
		- }
	- }

	- 修改reducers等等

	app.jsx
	- componentDidMount(){
		- 异步获取所有评论数据
		- this.
	- }

----------
	import {combineReducers} from ''
	- combineReducers 是一个函数

	- export default combineReducers({
		- counter, //指定..
		- comments
	- })
	## redux向外暴露的state是个什么结构？？
		- {counter:??,comments:[]}
	