## CSS
### 1. vw、vh 是什么？
vw 和 vh 是 CSS3 新单位，即 view width 可视窗口宽度 和 view height 可视窗口高度。1vw 就等于可视窗口宽度的百分之一，1vh 就等于可视窗口高度的百分之一。
### 2. BFC 及其应用
块级格式化上下文，指的是一个独立的布局空间，BFC内部的元素布局与外部互不影响。触发BFC的方式有：
 - 设置浮动
 - overflow设置为auto、scroll、hidden
 - position设置为absolute、fixed

常见的BFC应用有：
- 解决浮动元素令父元素高度塌陷
- 解决非浮动元素被浮动元素覆盖的问题
- 解决外边距垂直方向重合的问题

### 3. 原型和原型链
每个js对象(除null)都有一个__proto__属性，这个属性指向的就是该对象的原型。原型又有一个constructor属性，指向该关联的构造函数。构造函数的prototype属性指向函数的原型对象。
原型链：如果一个实例没有一个属性或方法，它就会去它的原型中寻找，如果它的原型中也没有，就会继续向上找， 直到最后一个找不到原型时返回null
### 4. this
箭头函数的this，就是包裹它的第一个普通函数中的this；普通函数：如果是new的方式，this绑定在实例上。如果是fn(),那么this就是window。如果是obj.fn()，那么this就是obj。bind，call，apply的this就是第一个参数
### 5. 数组去重
[...new Set(arr)]； Array.from(new Set(arr))； 双层循环+arr.splice； 新建数组，遍历arr，利用indexOf； 用includes； 用filter+indexOf； 利用map
### 6. 闭包
函数A中有一个函数B，B可以访问到函数A中的变量，那么函数B就是闭包。应用：
- 模拟块级作用域
- 做埋点统计
- 封装变量，避免变量污染

缺点：闭包会常驻内存，可能会造成内存泄漏
### Promise
promise是ES6新增的一种异步编程的解决方案，Promise本质上是一个绑定了回调的对象。解决了回调地狱的问题。Promise有三种状态：pending、fulfilled、rejected，其中初始状态是pending，可以通过函数resolve把状态变为fulfilled或者通过函数reject把状态变为rejected，状态一经改变就不能再次变化。有then、catch、finally三个方法。

prmoise.all()该方法接收一个可迭代对象（如Array,Map,Set），返回一个Promise（新期约），只有当该数组中所有的Promise完成后才会有pending转变为resolved执行then里面的回调函数；若数组中有任意一个promise被拒绝则会执行失败回调，即catch方法会捕获到首个被执行的reject函数。通过该方法获得的成功结果的数组里面的数据顺序和接收到的promise数组顺序是一致的。
### async 和 await
async和await是promise的语法糖，async函数返回的就是Promise对象。并且await只能配套async使用。
优势在于处理then的调用链，能够更清晰准确的写出代码，毕竟写一大堆then也很恶心，并且也能优雅地解决回调地狱问题。因为 await 将异步代码改造成了同步代码，如果多个异步代码没有依赖性却使用了 await 会导致性能上的降低。
### ajax、fetch、axios三者有什么区别？
Ajax(Asyn JavaScript and xml)是一个技术统称；fetch是一个浏览器原生api，和XmlHttpRequest是一个级别，语法更加简洁易用，支持promise；axios是一个npm第三方库；
### 防抖和节流
防抖：限制执行次数，多次密集执行只执行最后一次。应用：输入框
```
function debounce(fn, delay = 1000){
  let timer
  return function() {
    if(timer) clearTimeOut(timer)
    timer = setTimeout(()=>{
      fn.apply(this, arguments)
    }, delay)
  }
}
```
节流：限制执行频率，有节奏的执行 应用：滚动加载
```
function throttle(fn, delay = 1000){
  let timer
  return function() {
    if(timer) return
    timer = setTimeout(()=>{
      fn.apply(this, arguments)
    }, delay)
  }
}
```
### 箭头函数有什么缺点？什么时候不能使用箭头函数？
缺点：没有arguments；无法通过call，apply，bind改变this；
不能使用：对象的方法/原型的方法用箭头函数；构造函数；动态上下文中的函数；Vue的生命周期和method中也不能使用
### 请描述TCP三次握手和四次挥手
刚开始客户端处于 closed 的状态，服务端处于 listen 状态。

1、第一次握手：客户端给服务端发一个 SYN 报文，并指明客户端的初始化序列号 ISN（c）。此时客户端处于 SYN_Send 状态。

2、第二次握手：服务器收到客户端的 SYN 报文之后，会以自己的 SYN 报文作为应答，并且也是指定了自己的初始化序列号 ISN(s)，同时会把客户端的 ISN + 1 作为 ACK 的值，表示自己已经收到了客户端的 SYN，此时服务器处于 SYN_REVD 的状态。

3、第三次握手：客户端收到 SYN 报文之后，会发送一个 ACK 报文，当然，也是一样把服务器的 ISN + 1 作为 ACK 的值，表示已经收到了服务端的 SYN 报文，此时客户端处于 establised 状态。

4、服务器收到 ACK 报文之后，也处于 establised 状态，此时，双方以建立起了链接。

四次挥手：

1、第一次挥手：客户端发送一个 FIN 报文，报文中会指定一个序列号。此时客户端处于FIN_WAIT1状态。

2、第二次握手：服务端收到 FIN 之后，会发送 ACK 报文，且把客户端的序列号值 + 1 作为 ACK 报文的序列号值，表明已经收到客户端的报文了，此时服务端处于 CLOSE_WAIT状态。

3、第三次挥手：如果服务端也想断开连接了，和客户端的第一次挥手一样，发给 FIN 报文，且指定一个序列号。此时服务端处于 LAST_ACK 的状态。

4、第四次挥手：客户端收到 FIN 之后，一样发送一个 ACK 报文作为应答，且把服务端的序列号值 + 1 作为自己 ACK 报文的序列号值，此时客户端处于 TIME_WAIT 状态。需要过一阵子以确保服务端收到自己的 ACK 报文之后才会进入 CLOSED 状态

5、服务端收到 ACK 报文之后，就处于关闭连接了，处于 CLOSED 状态。
### for...in和for...of的区别？
for...in用于可枚举数据，如对象、数组、字符串，得到key
for...of用于可迭代数据，如数组、字符串、map、set，得到value
### offsetHeight、scrollHeight、clientHeight有什么区别？
offsetHeight：border + padding + content
clientHeight：padding + content
scrollHeight：padding + 实际内容尺寸
### HTMLCollection 与 NodeList 的区别
NodeList 是一个静态集合，其不受 DOM 树元素变化的影响；相当于是 DOM 树快照，节点数量和类型的快照，就是对节点增删，NodeList 感觉不到。但是对节点内部内容修改，是可以感觉到的，比如修改 innerHTML。

HTMLCollection 是动态绑定的，是一个的动态集合，DOM 树发生变化，HTMLCollection 也会随之变化，节点的增删是敏感的。

只有 NodeList 对象有包含属性节点和文本节点。

HTMLCollection 元素可以通过 name，id 或 index 索引来获取。NodeList 只能通过 index 索引来获取。

HTMLCollection 和 NodeList 本身无法使用数组的方法：pop()、push() 或 join() 等。除非你把他转为一个数组，上文有介绍到。
### vue的computed和watch的区别？
computed 是计算属性，依赖其他属性计算值，并且 computed 的值有缓存，只有当计算值变化才会返回内容。
watch 监听到值的变化就会执行回调，在回调中可以进行一些逻辑操作。一般来说需要依赖别的属性来动态获得值的时候可以使用 computed，对于监听到值的变化需要做一些复杂业务逻辑的情况可以使用 watch。这2个都支持对象的写法：watch：deep、immediate、handle；computed：get，set
### vuex中mutation和action的区别？
mutation必须同步代码；action可包含多个mutation，可包含异步代码
### JS内存垃圾回收用什么算法？
很早之前用引用计数，有缺陷：循环引用的问题；现代：标记清除

首先它会遍历堆内存上所有的对象，分别给它们打上标记，然后在代码执行过程结束之后，对所使用过的变量取消标记。在清除阶段再把具有标记的内存对象进行整体清除，从而释放内存空间。
V8 的垃圾回收策略主要基于分代式垃圾回收机制，V8 中将堆内存分为新生代和老生代两区域，采用不同的垃圾回收器也就是不同的策略管理垃圾回收。
新生代的对象为存活时间较短的对象，简单来说就是新产生的对象，通常只支持 1～8M 的容量，而老生代的对象为存活事件较长或常驻内存的对象，简单来说就是经历过新生代垃圾回收后还存活下来的对象，容量通常比较大。
### js内存泄漏如何检测？场景有哪些？
检测内存变化。利用Chrome devTools的performance和memory去检测，看heap是不是一直上升。
场景：
- 被全局变量、函数引用，组件销毁时未清除。
- 被全局事件、定时器引用，组件销毁时未清除。
- 被自定义事件引用，组件销毁时未清除。
### event loop
大家也知道了当我们执行 JS 代码的时候其实就是往执行栈中放入函数，那么遇到异步代码的时候该怎么办？其实当遇到异步的代码时，会被挂起并在需要执行的时候加入到 Task（有多种 Task） 队列中。一旦执行栈为空，Event Loop 就会从 Task 队列中拿出需要执行的代码并放入执行栈中执行，所以本质上来说 JS 中的异步还是同步行为。所以 Event Loop 执行顺序如下所示：

- 首先执行同步代码，这属于宏任务
- 当执行完所有同步代码后，执行栈为空，查询是否有异步代码需要执行
- 执行所有微任务
- 当执行完所有微任务后，如有必要会渲染页面
- 然后开始下一轮 Event Loop，执行宏任务中的异步代码，也就是 setTimeout 中的回调函数
### vue生命周期
在 beforeCreate 钩子函数调用的时候，是获取不到 props 或者 data 中的数据的，因为这些数据的初始化都在 initState 中。

然后会执行 created 钩子函数，在这一步的时候已经可以访问到之前不能访问到的数据，但是这时候组件还没被挂载，所以是看不到的。

接下来会先执行 beforeMount 钩子函数，开始创建 VDOM，最后执行 mounted 钩子，并将 VDOM 渲染为真实 DOM 并且渲染数据。组件中如果有子组件的话，会递归挂载子组件，只有当所有子组件全部挂载完毕，才会执行根组件的挂载钩子。

接下来是数据更新时会调用的钩子函数 beforeUpdate 和 updated，这两个钩子函数没什么好说的，就是分别在数据更新前和更新后会调用。

另外还有 keep-alive 独有的生命周期，分别为 activated 和 deactivated 。用 keep-alive 包裹的组件在切换时不会进行销毁，而是缓存到内存中并执行 deactivated 钩子函数，命中缓存渲染后会执行 actived 钩子函数。

最后就是销毁组件的钩子函数 beforeDestroy 和 destroyed。前者适合移除事件、定时器等等，否则可能会引起内存泄露的问题。然后进行一系列的销毁操作，如果有子组件的话，也会递归销毁子组件，所有子组件都销毁完毕后才会执行根组件的 destroyed 钩子函数。
### vue2和vue3的区别
- 生命周期：Vue3取消了beforeCreate和create，vue3都是hooks
- vue3可以写多个根节点
- Vue2 是选项API（Options API），一个逻辑会散乱在文件不同位置（data、props、computed、watch、生命周期钩子等），导致代码的可读性变差。当需要修改某个逻辑时，需要上下来回跳转文件位置。
Vue3 组合式API（Composition API）则很好地解决了这个问题，可将同一逻辑的内容写到一起，增强了代码的可读性、内聚性，其还提供了较为完美的逻辑复用性方案。
- Vue3 提供 Teleport 组件可将部分 DOM 移动到 Vue app 之外的位置。比如项目中常见的 Dialog 弹窗。
- Vue2 响应式原理基础是 Object.defineProperty；Vue3 响应式原理基础是 Proxy。主要原因：无法监听对象或数组新增、删除的元素。
Vue2 相应解决方案：针对常用数组原型方法push、pop、shift、unshift、splice、sort、reverse进行了hack处理；提供Vue.set监听对象/数组新增属性。对象的新增/删除响应，还可以new个新对象，新增则合并新属性和旧对象；删除则将删除属性后的对象深拷贝给新对象。Proxy 是 ES6 新特性，通过第2个参数 handler 拦截目标对象的行为。相较于 Object.defineProperty 提供语言全范围的响应能力，消除了局限性。
- Vue3 相比于 Vue2，虚拟DOM上增加 patchFlag 字段
- diff算法优化，主要还是patchFlag 帮助 diff 时区分静态节点，以及不同类型的动态节点。一定程度地减少节点本身及其属性的比对
- 打包优化
- Vue3 由 TypeScript 重写，相对于 Vue2 有更好的 TypeScript 支持。
### 描述从url到页面展示的完整过程
- DNS查询得到ip，建立TCP连接
- 浏览器发送HTTP请求
- 收到请求响应，得到HTML源码
- 解析HTML过程中，遇到静态资源还会继续发起网络请求
- HTML构建DOM树
- CSS构建CSSOM树，两者结合形成render tree
- 渲染render tree，计算绘制，同时执行js
### new一个对象的过程是什么？
- 创建一个空对象，继承构造函数的原型
- 执行构造函数(将obj作为this)
- 返回objvue
### call、apply、bind的区别？
- 三者都可以改变函数的this对象指向。
- 三者第一个参数都是this要指向的对象，如果如果没有这个参数或参数为undefined或null，则默认指向全局window。
- 三者都可以传参，但是apply是数组，而call是参数列表，且apply和call是一次性传入参数，而bind可以分为多次传入。
- bind 是返回绑定this之后的函数，便于稍后调用；apply 、call 则是立即执行 。

### vue有哪些优化？
- 图片懒加载
- v-for加key
- 使用keep-alive
- 路由懒加载
- 组件按需加载
- 开启gzip压缩
- Chrome Performance 查找性能瓶颈
### vue有哪些坑？
- 内存泄漏：全局变量、全部事件、全局定时器、自定义事件
- vue2响应式的缺陷：data新增属性用Vue.set,删除属性用Vue.delete
- 路由切换时scroll到顶部，解决方案：缓存数据和scrollTop的值，返回的时候scrollTo





















































