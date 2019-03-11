###  redux 处理异步需要redux-chunk插件

```javascript
npm install redux-devtools-extension  //开启插件
```

使用react-redux优雅的链接react和redux

// redux-saga可以代替 react-chunk

redux 有中间件机制 applyMiddleware开启中间件

 

```javascript
// index.js
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import * as serviceWorker from './serviceWorker';
import { createStore, applyMiddleware } from "redux"; //applyMiddleware 开启中间件
import App from './App';
import { counter, addGun, addGunAsync } from "./index.redux";
import thunk from "redux-thunk"; // 引入处理异步的redux中间件
const store = createStore(counter, applyMiddleware(thunk)) // 第二个参数applyMiddleware(thunk) 开启中间件
function render() {
    ReactDOM.render(<App  store =  {store} addGunAsync={addGunAsync} addGun={addGun} />, document.getElementById('root'))
}
render()
// 订阅后执行render函数
store.subscribe(render)
// ReactDOM.render(<App store = {store} />, document.getElementById('root'));

// If you want your app to work offline and load faster, you can change
// unregister() to register() below. Note this comes with some pitfalls.
// Learn more about service workers: https://bit.ly/CRA-PWA
serviceWorker.unregister();
```

```javascript
// index.redux.js
const ADD_GUN = '加机关枪'
const REMOVE_GUN = '减机关枪'
export function counter(state = 0, action) {
    switch (action.type) {
        case ADD_GUN:
            return state+1
        case REMOVE_GUN:
            return state - 1
        default:
            return 10
    }
}
// action creator
export function addGun() {
    return {type: ADD_GUN }
}
//
export function removeGun() {
    return{ type: REMOVE_GUN}
}
// 与其他不同的是返回了一个函数  异步写法
export function addGunAsync() {
    return dispatch => {
        setTimeout (() => {
            dispatch(addGun())
        }, 2000)
    }
}
```

```javascript
// app.js
import React from 'react';
import {Button} from "antd-mobile";
import 'antd-mobile/dist/antd-mobile.css'
 class App extends React.Component{
  render() {
    const store = this.props.store
    const num = store.getState()
    const addGun = this.props.addGun
    const addGunAsync = this.props.addGunAsync
    // const boss = '李云龙'
    return  (
        <div>
            <h2>现在有机枪, {num}</h2>
            <button onClick={ () => store.dispatch(addGun())}>aaa </button>
            <button onClick={ () => store.dispatch(addGunAsync ())}>异步 </button>
// 绑定异步方法
          {/*<Op name='涨到秒'></Op>*/}
          {/*<Childs name='aaa'></Childs>*/}
        </div>
    )
  }
}
function Childs(props) {
  return <h3>我是小弟 {props.name}</h3>
}
class Op extends React.Component{
  constructor (props) {
    super(props)
    this.state = {
       solders : ['1', '2', '3']
    }
    // this.addSolder = this.addSolder.bind(this)
  }
  addSolder () {
    this.setState({
      solders: [...this.state.solders, '新兵']
    })
  }
  render() {
    const boss = 'nihao'
    return (
        <div>
          <h2>{this.props.name}</h2>
          <Button type='primary' onClick={() => this.addSolder()}>aaa</Button>
          <ul>
            {this.state.solders.map(v => {
              return <li key={v}>{v}</li>
            })}
          </ul>
        </div>
    )
  }
  componentWillMount() {
    console.log('组件马上就要加载了')
  }
  componentDidMount() {
    console.log('组件加载完毕')
  }
}
export default App
```