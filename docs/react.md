
### 前端三大框架都是 面向数据编程 
### React使用虚拟DOM方法来解决真实DOM操作性能损耗问题



### 什么是虚拟DOM 
>虚拟DOM本质上就是一个JS对象<br> 
如下

    ['div', {id: 'abc'},['span', {}, 'hello world']]
    
>当内容有所修改时候<br> 
如下

    ['div', {id: 'abc'},['span', {}, 'YYYYYYYYYYY']]
    
> 使用Diff算法对比 找出原来虚拟DOM 和之后虚拟DOM的不同 进行修改

### ref属性
React使用虚拟DOM 但有时候我们需要组件实例的时候就用到了ref



### React语法JSX
>在JS中写入HTML、CSS、JS 即JSX

##### <App />就属于JSX语法

##### React中js文件里 使用JSX语法必须引入

    import React, { Component } from 'react';
    
    
##### React中js文件里 \<div\>就是JSX语法 并不是HTML标签

##### React中js文件里 JSX语法最外层必须都包层<div>

##### React中js文件里 如果想最外层\<div\>隐藏引入 Fragment 如下

    import React, { Component， Fragment } from 'react';
    
    包在<Fragment>   <div>换成<Fragment>


##### React中js文件里 首字母大写的是组件 小写的是元素

##### React中js文件里 \<div\>上写class 要写className="Class"

##### React中js文件里 迭代器中每个都要有key值 如下
key选择一个稳定的值

    <li key={index}>
   
    
##### React中js文件里 \<label\> 中for 用法冲突 要用htmlFor替代

##### React中js文件里 注释要这样写{/* 这里写注释*/}

##### React中js文件里 父子组件之间传值的方法 

>父组件引入子组件 import 子组件名字 from '子组件路径'; 使用<子组件名字>
>子组件 construtor里面定义过super(props); 使用this.props.xxx 
>父组件 方法要做一次this指向绑定 以handleBtnClick为例 如下

    this.handleBtnClick.bind(this)
  
    
##### React中js文件里 .propTypes  指定类型 .propDefault 默认指定
    
    

## 生命周期函数
[简书-生命周期函数======>https://www.jianshu.com/p/514fe21b9914](https://www.jianshu.com/p/514fe21b9914)
> 生命周期函数是指在某一个时刻组件会自动调用的函数


![liveCycle](https://note.youdao.com/yws/public/resource/e2f8ddd2f88f417a4a47e4b4984e66bc/6FE2BC24346F4BE3BEF9B819EC4EAF3F)


    initialization //初始化时调用
    mounting  //被创建或者被增加时调用
    updation //修改被改变更新时调用
    unmounting //移除时销毁时调用


### initialization 初始化时调用

#### mounting 被创建或者被增加时调用

- #### componentWillMount
>在组件挂载到DOM前调用，且只会被调用一次，在这边调用this.setState不会引起组件重新渲染，也可以把写在这边的内容提前到constructor()中，所以项目中很少用。

- #### render
>根据组件的props和state（无两者的重传递和重赋值，论值是否有变化，都可以引起组件重新render） ，return 一个React元素（描述组件，即UI），不负责组件实际渲染工作，之后由React自身根据此元素去渲染出页面DOM。render是纯函数（Pure function：函数的返回结果只依赖于它的参数；函数执行过程里面没有副作用），不能在里面执行this.setState，会有改变组件状态的副作用。

- #### componentDidMount
>组件挂载到DOM后调用，且只会被调用一次

### updation 修改被改变更新时调用
造成更新有三种情况
- #### componentWillReceiveProps(nextProps)
>此方法只调用于props引起的组件更新过程中，参数nextProps是父组件传给当前组件的新props。但父组件render方法的调用不能保证重传给当前组件的props是有变化的，所以在此方法中根据nextProps和this.props来查明重传的props是否改变，以及如果改变了要执行啥，比如根据新的props调用this.setState出发当前组件的重新render

- #### shouldComponentUpdate(nextProps, nextState)
>此方法通过比较nextProps，nextState及当前组件的this.props，this.state，返回true时当前组件将继续执行更新过程，返回false则当前组件更新停止，以此可用来减少组件的不必要渲染，优化组件性能。
>ps：这边也可以看出，就算componentWillReceiveProps()中执行了this.setState，更新了state，但在render前（如shouldComponentUpdate，componentWillUpdate），this.state依然指向更新前的state，不然nextState及当前组件的this.state的对比就一直是true了。

- #### componentWillUpdate(nextProps, nextState)
>此方法在调用render方法前执行，在这边可执行一些组件更新发生前的工作，一般较少用

- #### render
>render方法在上文讲过，这边只是重新调用。
>componentDidUpdate(prevProps, prevState)
>此方法在组件更新后被调用，可以操作组件更新的DOM，prevProps和prevState这两个参数指的是组件更新前的props和state

- #### componentDidUpdate

- #### 1.父组件重新render
>a.可通过shouldComponentUpdate方法优化
>b.在componentWillReceiveProps方法中，将props转换成自己的state
- ##### 2.组件本身调用setState
>可通过shouldComponentUpdate方法优化。


### unmounting 移除时销毁时调用
- #### componentWillUnmount
>此方法在组件被卸载前调用，可以在这里执行一些清理工作，比如清除组件中使用的定时器，清除componentDidMount中手动创建的DOM元素等，以避免引起内存泄漏。

#### 版本更新---下图
![5287253-82f6af8e0cc9012b](https://note.youdao.com/yws/public/resource/e2f8ddd2f88f417a4a47e4b4984e66bc/59A2C9DD1ABA4FD29E136E95DF062270?ynotemdtimestamp=1559701909603)
<br>
![5287253-ccb5d35ca1defefc](https://note.youdao.com/yws/public/resource/e2f8ddd2f88f417a4a47e4b4984e66bc/07EA5E9FCD14472FA21B19A45BD835BF)
<br>

    //一个组件要从父组件接受参数
    //如果这个组件第一个存在于父组件中，不会执行
    //如果这个组件之前已经存在于父组件中，才会执行
    componentWillReceiveProps(){}

    什么生命周期函数都可以删renter必须留不然会报错
    
shouldComponentUpdate

<br>
<br>
<br>

# Redux 概念 

### Redux 就是把组件之间的数据放到一个公用的地方去存储 (Store)
### 解决了父子组件直接传值繁琐的问题


![Redux](https://note.youdao.com/yws/public/resource/e2f8ddd2f88f417a4a47e4b4984e66bc/C93191F3A3EE4C009CF2BBC5712EB77C)

### Redux = Reducer + Flux

![Redux Flow](https://note.youdao.com/yws/public/resource/e2f8ddd2f88f417a4a47e4b4984e66bc/D20A3CA821334AD4B18527FC9BE97A4D)

<br>
<br>
<br>

>store 是唯一的 全局只有一个
<br>
>只有store自己才能改变自己
<br>
>reducer 必须是纯函数
<br>
>注：纯函数是指。给固定的输入，就一定会有固定的输出，而且不会有任何副作用
<br>
>所以 reducer 可以接受state,但绝对不能修改state

    createStor //创建一个Store
    store.dispatch //派发action传递信息给store
    store.getState //获取store所有数据内容
    store.subscribe //订阅store的改变



#### <center> --2019/5/12-- </center>
