# VUEX
>*  不能直接改变store中的状态.改变store中的状态的唯一途径是显示的提交 (commit) mutation 
>* 单一状态树 用一个对象包含了全部的应用层级的状态
>* 在store实例中读取状态最简单的方法是用<i style="color:red">计算属性 </i>  

![](https://raw.githubusercontent.com/LFmadongsheng/imagesBed/master/img/20180919155248.png) 

>* mapState 辅助函数 (在组件需要获取多个状态时使用)

![](https://raw.githubusercontent.com/LFmadongsheng/imagesBed/master/img/20180919160129.png)

>* 当映射的计算属性的名称与state的子节点名称相同时,也可以给mapState传一个字符串数组

![](https://raw.githubusercontent.com/LFmadongsheng/imagesBed/master/img/20180919160903.png)

>* mapState函数返回的时一个对象. 运用对象展开符将他与局部计算属性混合使用

![](https://raw.githubusercontent.com/LFmadongsheng/imagesBed/master/img/20180919161320.png)

>* getter  可以认为是store的计算属性

### Getter 接受state作为第一个参数

![](https://raw.githubusercontent.com/LFmadongsheng/imagesBed/master/img/20180919163039.png)

<attr style="color:gold">通过属性访问</attr>

Getter会暴露为store.getters对象 可以用属性的形式访问这些

>* Getter 也可以接受其他getter作为第二个参数

![](https://raw.githubusercontent.com/LFmadongsheng/imagesBed/master/img/20180919163521.png)

<red style="color:gold">注意: getter 在通过属性访问时是作为 Vue 的响应式系统的一部分缓存其中的</red>

### 通过方法访问
通过让getter返回一个函数,来实现给getter传参

![](https://raw.githubusercontent.com/LFmadongsheng/imagesBed/master/img/20180919164439.png)

<red style="color:gold">注意: getter 在通过方法访问时，每次都会去进行调用，而不会缓存结果</red>

## mapGetters 辅助函数

mapGetters 辅助函数仅仅是将 store 中的 getter 映射到局部计算属性

![](https://raw.githubusercontent.com/LFmadongsheng/imagesBed/master/img/20180919164913.png)


## 更改vuex的store中的状态的唯一方法是提交mutation 

每个mutation都有一个字符串的事件类型(type)和一个回调函数(ahndler) 这个回调函数实际上就是状态更改的地方,并且接受state作为第一个参数
![](https://raw.githubusercontent.com/LFmadongsheng/imagesBed/master/img/20180919165523.png)

你不能直接钓同一个mutation handler 这个更像是事件注册 当触发一个类型为 increment 的mutation 时,
调用此函数. 要唤醒一个mutation handler 你需要以相应的type调用 store.commit方法

![](https://raw.githubusercontent.com/LFmadongsheng/imagesBed/master/img/20180919165944.png)

提交载荷 (Payload)
你可以向store.commit传入额外的参数,即mutation的荷载

![](https://raw.githubusercontent.com/LFmadongsheng/imagesBed/master/img/20180919170208.png)

在大多数情况下,荷载应该是一个对象,这样可以包含多个字段并且记录mutation会更已读

![](https://raw.githubusercontent.com/LFmadongsheng/imagesBed/master/img/20180919170749.png)

对象风格的提交方式

提交mutation的另一种方式是直接使用包含type属相的对象

![](https://raw.githubusercontent.com/LFmadongsheng/imagesBed/master/img/20180919171710.png)

## Mutation 需遵守Vue的响应规则

### 1. 最好提前在你的store中的初始化好所有所需属性
### 2. 当需要在对象上添加新属性时,应该
    使用Vue.set(obj, 'newProp',123), 或者
    以新对象替换老对象.例如

 ![](https://raw.githubusercontent.com/LFmadongsheng/imagesBed/master/img/20180919174205.png)

## 使用常量代替Mutation事件类型

![](https://raw.githubusercontent.com/LFmadongsheng/imagesBed/master/img/20180919174943.png)

## mutation 必须是同步函数
在组件中提交mutation

你可以在组件中使用 this.$store.commit('xxx') 提交 mutation，或者使用 mapMutations 辅助函数将组件中的 methods 映射为 store.commit 调用（需要在根节点注入 store）

![](https://raw.githubusercontent.com/LFmadongsheng/imagesBed/master/img/20180919180252.png)

# Action 
>* Action 提交的是mutation,而不是直接变更状态
>* Action可以包含任意一步操作

注册一个action

![](https://raw.githubusercontent.com/LFmadongsheng/imagesBed/master/img/20180919180917.png)

Action 函数接受一个与store实例具有相同方法和属性的context对象,因此可以调用context.commit提交一个mutation ,或者通过context.state 和context.getter 来获取state和getters 

![](https://raw.githubusercontent.com/LFmadongsheng/imagesBed/master/img/20180920102024.png)

# 分发Action 

Action 通过store.dispatch方法触发

store.dispatch('increment')

action内部可以执行异步操作

![](https://raw.githubusercontent.com/LFmadongsheng/imagesBed/master/img/20180920102419.png)

## Action 支持同样的载荷方式 和  对象方式 进行分发

![](https://raw.githubusercontent.com/LFmadongsheng/imagesBed/master/img/20180920102638.png)

## 在组件中分发Action

你在组件中使用 <strong style="color:gold">this.$store.dispatch('xxx')</strong>分发action 或者使用mapActions 辅助函数将组件的methods映射为 store.dispatch 调用(需要现在根节点注入store)

![](https://raw.githubusercontent.com/LFmadongsheng/imagesBed/master/img/20180920103448.png)

# 组合Action 

Action通常是异步的,当需要组合多个action的时候,要明白 store.dispatch可以处理被触发的action的处理函数返回的Promise, 并且 仍旧返回Promise

![](https://raw.githubusercontent.com/LFmadongsheng/imagesBed/master/img/20180920104542.png)

现在你可以 

![](https://raw.githubusercontent.com/LFmadongsheng/imagesBed/master/img/20180920104801.png)

在另外一个Action 中也可以

![](https://raw.githubusercontent.com/LFmadongsheng/imagesBed/master/img/20180920104926.png)

利用async/await 可以如下组合action

![](https://raw.githubusercontent.com/LFmadongsheng/imagesBed/master/img/20180920105051.png)

