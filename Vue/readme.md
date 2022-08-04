#  Map 和 Set 的区别？
1. Map是键值对，Set是值得集合，当然键和值可以是任何的值；

2. Map可以通过get方法获取值，而set不能因为它只有值；

3. 都能通过迭代器进行for...of遍历；

4. Set的值是唯一的可以做数组去重，Map由于没有格式限制，可以做数据存储；


# Map 和 Object的区别？
1. Map中的键是有序的（FIFO原则），而添加到对象中的键则不是。
2. Map中的键值对个数可以从size属性获取，而添加到对象中的键则不是。
3. 一个Object的键只能是字符串或者Symbols，但是一个Map的键可以是任意值。

Map对象的方法：
- set(key,val): 向Map中添加新元素。
- get(key,val): 通过键值查找特定的数值并返回。
- has（key,val: 通过Map对象中是否有Key所对应的值，有返回true，否则返回false。
- delete(key): 通过键值从Map中移除对应的数据。
- clear（）：将这个Map中的所有元素删除

Map对象的遍历方法：
- keys(): 返回键名的遍历器
- values(): 返回键值的遍历器
- entries(): 返回键值对的遍历器
- forEach(): 使用回调函数遍历每个成员


# 数组的filter、every、flat的作用是什么？
1. filter(): 对数组中的每一项运行给定函数，返回该函数会返回true的项组成的数组。
2. every():  对数组中的每一项运行给定函数，如果该函数对每一项都返回true，则返回true。
3. flat():   会按照一个可指定的深度递归遍历数组，并将所有元素与遍历到的子数组中的元素合并成一个新的数组返回。

# promise.all 和 promise.race区别
1. promise.all 接收多个promise包装成一个新的promise，成功返回的是成功的数据，失败返回的是失败的数据，一但失败不会继续执行
2. promise.race 有任意一个返回成功后，就算完成。哪个结果获取的最快，就返回哪个结果。不管返回的结果是成功还是失败。
使用场景
1. all ：一个操作同时需要好几个接口里边的返回数据
2. race：好几个接口会返回一样的数据，哪个接口的数据先返回就使用哪个接口的数据

# new的实现原理
四步骤：
1. 创建一个新对象
2. 链接到原型（将构造函数的prototype赋值给新对象的 __proto__）
3. 绑定this（构造函数中的this指向新对象并且调用构造函数）
4. 返回新对象

# 怎么画一条0.5px的边
1. 直接设置0.5px 
2. 缩放  height: 1px; transform: scaleY(0.5); transform-origin: 50% 100%;
3. 线性渐变linear-gradient  height: 1px; background: linear-gradient(0deg, #fff, #000);
  （1px的逻辑像素代表的是物理（设备）有2px，由于是线性渐变，所以第一个px只能是#fff，第二个px只能是#000 从白色渐变到黑色）
4.  box-shadow   height: 1px; background: none;  box-shadow: 0 0.5px 0 #000;

# ES6新增特性

# 盒模型(由content、padding、border、margin构成)
- 标准盒模型：只包含content
- IE盒模型： content + padding + border

# CSS选择器和优先级

# 重排和重绘
- 重排：无论通过什么方式影响了元素的集合信息（元素在视口内的位置和尺寸大小），浏览器需要重新计算元素在视口内的几何属性，这个过程叫做重排。
- 重绘：通过构造渲染树和重排（回流）阶段，我们知道了哪些节点是可见的，以及可见节点的样式和具体的几何信息（元素在视口内的位置和尺寸大小），接下来就可以将
渲染树的每个节点都转化为屏幕上的实际像素，这个阶段叫做重绘。
如何减少重拍和重绘？
1. 最小化重绘和重排：比如样式集中改变，使用添加新样式类名 .class 或 cssText
2. 批量操作DOM，比如读取某元素offsetWidth属性存到一个临时变量，再去使用。
3. 使用 absolute 或  fixed 使元素脱离文档流
4. 开启GPU加速，利用css属性transform、will-change等，比如改变元素位置，我们使用translate会比使用绝对定位改变其left、top等来的高效。因为它不会
触发重排或重绘IU，transform使浏览器元素创建一个GPU图层，这使得动画元素在一个独立的的层中进行渲染。当元素的内容没有发生改变，就没有必要进行重绘。



# 深拷贝
1. 用 new obj.constructor() 构造函数新建一个空对象而不用{}或者[]，这样可以保持原型链的继承。
2. 用obj.hasOwnProperty(key)来判断属性是否来自原型链上，因为for...in..也会遍历其原型链上的可枚举属性。

# 0.1 + 0.2 !== 0.3,讲讲 IEEE754，如何让其相等？
原因：
1. 进制转换：js在数字计算的时候，0.1和0.2都会被转成二进制后无限循环，但是js采用的IEEE754二进制浮点运算，最大可以存储53位有效数字，于是大于53位后面的全部会被截掉，将导致精度缺失。
2. 对阶运算“由于指数位数不相同，运算时需要对阶运算，阶小的尾数要根据差来右移（0舍1入），尾数位移时可能会发生数丢失的情况，影响精度。


# web存储
- cokkie：存储大小为4KB、http请求时需要发送到服务端，增加请求数量。只能用document.cokkie = '...' 来修改，太过简陋。
- localStorage、sessionStorage
 1. HTML5专门为存储来设计的，最大可存5M。
 2. API简答易用，setItem getItem
 3. 不会随着http请求被发送到服务端。

它们的区别：
1. localStorage 数据会永久存储，除非代码删除或者手动删除
2. sessionStorage 数据只存在于当前会话，浏览器关闭则清空。
3. 一般用localStroage多一些


# 状态码
- 1xx  服务器收到请求
- 2xx  请求成功，如200
- 3xx  重定向，如302
- 4xx  客户端错误，如404
- 5xx  服务端错误。如500


# 缓存策略（强制缓存、协商缓存）


# GET 和 POST 的区别
1. 从缓存的角度，GET请求会被浏览器主动缓存下来，留下历史记录，而POST默认不会。
2. 从编码的角度，GET只能进行URL编码，只能接收ASCLL字符，而POST没有限制。
3. 从参数的角度，GET一般放在URL，因此不安全，POST放在请求体中，更适合传输敏感信息。
4. 从幂等性的角度，GET是幂等的，而POST不是。（幂等表示执行相同的操作，结果也是相等的）。
5. TCP的角度，GET请求会把请求报文一次性发出去，而POST会分为两个TCP数据包，首先发header部分，如果服务器响应100（continue），然后发body部分。（火狐浏览器除外，它的POST请求只发一个TCP包）

# React生命周期
1. 初始化阶段（发生在constructor中的内容，在constructor中进行state、props的初始化，在这个阶段改state，不会执行更新阶段的生命周期，可以对state赋值）
2. 挂载阶段
  - componentWillMount 发生在render函数之前，还没有挂载Dom
  - render
  - componentDidMount  发生在render函数之后，已经挂载DOM
3. 更新阶段
  - componentWillReceiveProps（nextProps，nextState） 这个生命周期主要为我们提供对props发生改变的监听，如果你需要在props发生改变后，相应改变组件的一些state。在这个方法中改变state不会二次渲染，而是直接合并state
  - shouldComponentUpdate(nextProps,nextState)
  - componentWillUpdate(nextProps,nextState)
  - componentDidUpdate(preProps,preState )

4. 卸载阶段


# 前段性能优化
1. 减少HTTP请求
2. 将CSS放在文件头部，JavaScript文件放在底部
3. 减少重排重绘
4. 图片优化
5. 压缩文件
6. 善用缓存，不重复加载相同资源
7. 使用事件代理
8. 静态资源使用CDN
9. 使用服务器端渲染
10. 防抖节流
11. vue组件中使用keep-alive保存组件状态
12. webpack按需加载代码--Tree-Shaking
13. 使用Web Works
14. Vue首屏优化


