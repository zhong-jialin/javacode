---
title: "React的jsx"
date: 2023-03-06T14:04:54+08:00
categories: [
    "React",
]
---
## jsx语法规则
1. 定义标签不要写引号
2. 语句中有引用JS要用{}包起来
3. 样式指定的类名要用className
4. 内联样式要用 style:{{color:'white'}}
5. 单标签要闭合 '< input type = 'text'\>'
6. 自定义标签首字母要大写
7. 根标签只有一个

## React jsx语法示例
```
<body>
<div id="test"></div>
</body>
<script type="text/babel">
  const myId = 'zhong'
  const myDate = 'hellow'
  //创建虚拟DOM
  const VDOM = (
          <div>
            <h2 className="title" id={myId.toLocaleLowerCase()}>
              <span style={{color:'white',fontSize:'29px'}}>{myDate.toLocaleUpperCase()}</span>
            </h2>
            <input type="text"/>
          </div>
  )
  //渲染虚拟dom到页面
  ReactDOM.render(VDOM,document.getElementById('test'))
</script>
</html>
```
### 用jsx语法循环一个数组
```
<script type="text/babel">
  const title = '循环'
  const data = ['Angle','Vue','React']
  //创建虚拟DOM
  const VDOM = (
          <div>
            <h1>{title}</h1>
            <ul>
              {
                data.map((item,index)=>{
                  return <li key={index}>{item}</li>
                })
              }
            </ul>
          </div>
  )
  //渲染虚拟dom到页面
  ReactDOM.render(VDOM,document.getElementById('test'))
</script>
```
### 创建自定义函数式组件
```
<div id="test"></div>
</body>
<script type="text/babel">
  //定义组件
  function  Demo(){
    return <h2>自定1义组件</h2>
  }
  //渲染虚拟dom到页面
  ReactDOM.render(<Demo/>,document.getElementById('test'))
</script>
</html>
```
### 创建类式组件
```
<div id="test"></div>
</body>
<script type="text/babel">
    //定义组件
    class Welcome extends React.Component {
        render() {
            return <h1>Hello, {this.props.name}</h1>;
        }
    }
    //渲染虚拟dom到页面
    ReactDOM.render(<Mycomponent/>,document.getElementById('test'))
</script>
</html>
```
### 组件的state状态 绑定点击按钮
```
<script type="text/babel">
    //定义组件
    class Welcome extends React.Component {
       //方法初始化尽量不要在构造器里面
        constructor(props) {
            super(props);
            this.state = {isHot:false}
            //onclick 穿this过来重新绑定this
            this.chamgeweather = this.chamgeweather.bind(this)
        }
        chamgeweather(){
            //chamgeweather 的实例原型是welcome this只想Welcome
            //由于chamgeweather是由onclick调用，所以不能直接调用，会返回undefine

            //更改属性不能直接更改 例如
            // const isHot = this.state.isHot
            // this.state.isHot = ! isHot
            const isHot = this.state.isHot
            //这是一种合并动作
            this.setState({isHot:!isHot})
        }
        render() {
            return <h1 onClick={this.chamgeweather}>Hello{this.state.isHot?"1":"0"}</h1>;
        }
    }  //渲染虚拟dom到页面
    ReactDOM.render(<Welcome/>,document.getElementById('test'))
    //构造器只调用一次

</script>
```
### 简化上面的state
```
<script type="text/babel">
  //定义组件
  class Welcome extends React.Component {
    //方法初始化尽量不要在构造器里面
    constructor(props) {
      super(props);
    }
    state = {isHot:false,states:'wind'}
    render() {
      //接受两个属性
      const {isHot,states} = this.state
      //方法在welcome实例中 要使用this指向函数方法
      return <h1 onClick={this.chamgeweather}>Hello{isHot?"1":"0"},{states}</h1>;
    }
    //静态变量
    chamgeweather = ()=>{
      const isHot = this.state.isHot
      this.setState({isHot:!isHot})
    }
  }  //渲染虚拟dom到页面
  ReactDOM.render(<Welcome/>,document.getElementById('test'))

</script>
```
## props 传值 定义规则 需要引入props规则链接
```
<script type="text/babel">
  //定义组件
  class Person extends React.Component{
    render(){
      console.log(this)
      const {name,age,sex} = this.props
      return(
              <ul>
                <li>名字:{name}</li>
                <li>年龄:{age+1}</li>
                <li>性别:{sex}</li>
              </ul>
      )
    }
  }
  //给React加规则
  Person.propTypes = {
    //具体规则 只能传String类型数据
    //isRequired 必须传值不然会报错
    name: PropTypes.string,
    sex:PropTypes.string,
    age:PropTypes.number,
    speak:PropTypes.func

  }
  Person.defaultProps = {
    sex:'手扶拖拉机',
    age:99
  }
  //渲染虚拟dom到页面
  const p = {name:'laoliu', age : 19}
  const p2 = {name:'laoliu', sex:'白天男人，晚上女人'}
  ReactDOM.render(<Person {...p}/>,document.getElementById('test'))
  ReactDOM.render(<Person {...p2}/>,document.getElementById('test3'))
  //渲染时传值
  ReactDOM.render(<Person name ='nvmao'  speed="1" age={19} sex="man"/>,document.getElementById('test2'))
</script>
```
### 简写props传值
1
