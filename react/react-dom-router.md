**第一次学习react,刚用react-create-app搭建了一个项目第一点想先去找路由**

于是乎百度搜索了一下react的路由, 找到了react-dom-router

```
npm i react-router-dom -s
```

 [官方文档](https://reacttraining.com/react-router/web/guides/quick-start)  翻阅了下

首先看到的是如下代码

```javascript
import React from "react";
import { BrowserRouter as Router, Route, Link } from "react-router-dom";

function Index() {
  return <h2>Home</h2>;
}

function About() {
  return <h2>About</h2>;
}

function Users() {
  return <h2>Users</h2>;
}

function AppRouter() {
  return (
    <Router>
      <div>
        <nav>
          <ul>
            <li>
              <Link to="/">Home</Link>
            </li>
            <li>
              <Link to="/about/">About</Link>
            </li>
            <li>
              <Link to="/users/">Users</Link>
            </li>
          </ul>
        </nav>

        <Route path="/" exact component={Index} />
        <Route path="/about/" component={About} />
        <Route path="/users/" component={Users} />
      </div>
    </Router>
  );
}

export default AppRouter;

```

wtf? 最开始的时候有点蒙圈.因为在使用vue-router的时候都定义在一个公用文件里面然后注入vue实例。

仔细阅读了下

```javascript
 <Router>
      <div>
        <nav>
          <ul>
            <li>
              <Link to="/">Home</Link>
            </li>
            <li>
              <Link to="/about/">About</Link>
            </li>
            <li>
              <Link to="/users/">Users</Link>
            </li>
          </ul>
        </nav>

        <Route path="/" exact component={Index} />
        <Route path="/about/" component={About} />
        <Route path="/users/" component={Users} />
      </div>
    </Router>
```

似乎跟render dom放在了一起 用router 包裹一下  

```javascript
 <Route path="/" exact component={Index} />
```

这部分就是在定义路由 指定对应组件

于是乎在代码尝试之前翻阅了一篇博客 最后用下列方式定义好了路由

```javascript
// index.js
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import {HashRouter} from 'react-router-dom';
import * as serviceWorker from './serviceWorker';
ReactDOM.render(
    (<HashRouter>
        <App />
    </HashRouter>),
    document.getElementById('root'));

// If you want your app to work offline and load faster, you can change
// unregister() to register() below. Note this comes with some pitfalls.
// Learn more about service workers: http://bit.ly/CRA-PWA
serviceWorker.unregister();

```

```javascript
import React, { Component } from 'react';
import logo from './logo.svg';
import './App.css';
import {HashRouter, Route, Switch} from 'react-router-dom';
import Detail from './detail/detail';
class App extends Component {
  render() {
    return (
      <div className="App" id="root">
        <header className="App-header">
          <img src={logo} className="App-logo" alt="logo" />
          <p>
            Edit <code>src/App.js</code> and save to reload.
          </p>
          <a href="/#/detail">aa</a>
        </header>
        <Switch>
          {/*<Route exact path="/" component={App}/>*/}
          <Route exact path="/detail" component={Detail}/>
        </Switch>
      </div>
    );
  }
}

export default App;

```

以上是学习react的第一天 可能设置路由这块并不完善 期望下列学习中可以找到更好的办法

