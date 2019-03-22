## redux 调试工具

应用商店搜索redux 加入扩展程序 Redux DevTools

```javascript
import { createStore, applyMiddleware, compose } from "redux";

```

导入compose 

```javascript
const reduxDevtools = window.devToolsExtension? window.devToolsExtension():f => f

```

定义工具

```javascript
const store = createStore(counter, compose(
    applyMiddleware(thunk),
    reduxDevtools
))
```

定义store时候这么写

npm run eject 报错的解决方法 Remove untracked files, stash or commit any changes, and try again.

```
先

git add .
然后

git commit -m "init"
然后再npm run eject
```

```javascript
npm install babel-plugin-transform-decorators-legacy -s  支持redux 装饰器方式
```

## 使用react-redux

1. Provider react-redux 重要的俩点  Provider content 

```
index.js
import { Provider } from 'react-redux';
ReactDOM.render(
    (<Provider store={store}> // 将store 注入到 Provider
        <App   />
    </Provider>),
    document.getElementById('root')
)
```

```
// app.js
import React from 'react';
import {Button} from "antd-mobile";
import 'antd-mobile/dist/antd-mobile.css'
import { connect } from "react-redux";
import {addGun, removeGun , addGunAsync} from "./index.redux"; // 导入方法
const mapStatetoProps  = (state)=>{
    return {num: state}
}
const actionCreators = {addGun, removeGun , addGunAsync}
// 此处为装饰器模式 将data与action注入到App
@connect(mapStatetoProps, actionCreators)
class App extends React.Component{
  render() {
    const store = this.props.store // 此处变更获取方式
    const num = this.props.num
    const addGun = this.props.addGun
    const addGunAsync = this.props.addGunAsync
    // const boss = '李云龙'
    return  (
        <div>
            <h2>现在有机枪, {num}</h2>
            <button onClick={addGun}>aaa </button> // 此处变更事件方式
            <button onClick={ addGunAsync}>异步 </button>
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