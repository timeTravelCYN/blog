# 虚拟DOM

1. state 数据
2. 模板
3. 数据 + 模板 生成真实 DOM
4. state 发生改变
5. 数据 + 模板 结果，生成真实的 DOM， 替换原始的 DOM

缺陷：

1. 第一次生成了一个完整的 DOM 片段
2. 第二次生成了一个完整的 DOM 片段
3. 第二次的 DOM 替换第一次的 DOM， 非常耗性能

## 优化一下

1. state 数据
2. JSX 模板
3. 数据 + 模板 结合， 生成真实的 DOM， 来显示
4. state 发生改变
5. 数据 + 模板 结合，生成真实的 DOM， 并不直接替换原始的 DOM
6. 新的 DOM (DocumentFragment) 和原始的 DOM 作比对，找差异
7. 找出发生了变化的 DOM 元素
8. 只用新的 DOM 中的对应元素，替换掉老的 DOM 中的变化了的元素

缺陷：

DOM 替换变少了，节约了性能，但是比对又耗费了性能，性能提升并不明显

1. state 数据
2. JSX 模板
3. 数据 + 模板 生成虚拟 DOM (虚拟 DOM 就是一个 JS 对象， 用它来描述真实 DOM)
```js
['div', {id: 'abc'}, ['span',{}, 'hello']]
```
4. 用虚拟 DOM 的结构来生成真实的 DOM， 来显示
```html
<div id="abc"><span>hello</span></div>
```
5. state 发生变化
6. 数据 + 模板 生成新的虚拟 DOM， 极大的提升了性能
```js
['div', {id: 'abc'}, ['span',{}, 'bye bye']]
```
7. 比较 原始虚拟 DOM 和新的虚拟 DOM 的区别，找到区别是 span 中的内容
8. 直接操作 DOM ，改变 span 中的内容

DOM 相关的操作，耗费性能， js创建对象，则性能消耗小。

JSX 模板 -> JS 对象(虚拟 DOM ) -> 真实的 DOM 

虚拟 DOM 优点：

1. 性能提升了， DOM 比对被类比到了 JS 对象比对
2. 它使得跨端应用得以实现

## diff 算法

# 生命周期函数

> 生命周期函数指在某一个时刻组件会自动调用的函数

* componentWillMount 组件即将被挂载到页面的时刻自动执行
* render 页面渲染的时候执行
* componentDidMount 组件被挂载到页面之后被执行
* componentWillReceiveProps 一个组件从父组件接收参数，只要父组件的 render 函数被执行了，子组件的这个生命周期函数就会被执行
* shouldComponentUpdate 组件被更新之前执行 必须返回一个 bool， 代表是不是需要执行 update
* componentWillUpdate 组件将要更新之前执行
* componentDidUpdate 组件更新完成之后执行，做ajax请求的发送
* componentWillUnmount 当组件即将被从页面中剔除的时候，被执行

shouldComponentUpdate 会接受两个参数， nextProps, nextState 可以去判断是不是需要更新，借助这个方法可以避免无谓的 render 运行

## 使用场景







