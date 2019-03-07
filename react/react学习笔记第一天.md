####  create-react-app 脚手架

```javascript
npm run eject 弹出配置文件,可以自定义配置webpack
```

基础语法

- import React
- class语法新建组件,render里直接使用
- render函数返回值就是jsx语法,会把jsx转成js执行

```javascript
function a (props) {
    return <h2>hello, {props.a}<h2>
}
实际专换成
function a (props) {
    return React.createElement(
       h2,
       null,
       "hello",
       props.a
    )
}
```

view层语法

- js直接写html

- class要写成className
- 变量用{}包裹即可

```javascript
import React from 'react';
class App extends React.Component{
  render() {
      // 定义变量
    const boss = '李云龙'
    return  (
        <div>
          <h2>独立团, {boss}</h2> //赋值
          <Op name='涨到秒'></Op> // 引用组件并给组件传值
          <Childs name='aaa'></Childs>// 引用组件并给组件传值 函数式组件
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
    this.state = {   // 定义一个state 
       solders : ['1', '2', '3']
    }
      // 改变指针的另一种方式
    // this.addSolder = this.addSolder.bind(this)
  }
  addSolder () {
      // 修改state 本身的指针不会指向类
    this.setState({
      solders: [...this.state.solders, '新兵']
    })
  }
  render() {
    const boss = 'nihao'
    return (
        <div>
          <h2>{this.props.name}</h2>
          <button onClick={() => this.addSolder()}>aaa</button> // 调用函数并且把指针指向类本身
          <ul>
        // 遍历循环
            {this.state.solders.map(v => {
              return <li key={v}>{v}</li>
            })}
          </ul>
        </div>
    )
  }
  // 生命周期
  componentWillMount() {
    console.log('组件马上就要加载了')
  }
  componentDidMount() {
    console.log('组件加载完毕')
  }
}
export default App


```

![1551971385440](C:\Users\Dell\AppData\Roaming\Typora\typora-user-images\1551971385440.png)



 上图是react的生命周期

