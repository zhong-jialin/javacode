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
    class Mycomponent extends React.Component(){
        render(){
            console.log(this)
            return <h2>自定1义组件</h2>
        }
    }
    //渲染虚拟dom到页面
    ReactDOM.render(<Mycomponent/>,document.getElementById('test'))
</script>
</html>
```