### react-router-dom分为俩种模式

#### BrowserRouter 正常模式

#### hashRouter  哈希模式

react-router-dom分为Link，Route，Redirect，Switch

#### Link

- 跳转的标签 类似于 vue-router的  router-link

#### Redirect 

- 重定向组件, 放在route最下面

#### switch

- ```
  只渲染命中的第一个route
  ```

#### Route

- excat属性完全匹配
- path 匹配的路径
- component对应的组件

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
import Auth from './auth'
import Dashboard from './Dashboard'
import { BrowserRouter, Route, Link, Redirect, Switch} from "react-router-dom";
class Test extends React.Component{
    constructor (props) {
        super(props)
    }
    render () {
        console.log(this.props)
        return <h2>测试组件</h2>
    }
}
ReactDOM.render(
    (<Provider store={store}>
        <BrowserRouter>
            <Switch>
                {/*{只渲染命中的第一个route}*/}
                {/*<Redirect to='/qibinglian'></Redirect>*/}
                <Route path='/login' exact component ={Auth}></Route>
                <Route path='/dashboard' component ={Dashboard}></Route>
                <Redirect to='dashboard'/>
                {/*<Route path='/qibinglian' component ={qibinglian}></Route>*/}
            </Switch>
        </BrowserRouter>
    </Provider>),
    document.getElementById('root')
)

```

