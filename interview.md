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
