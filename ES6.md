j



## **ES6**

let、const、箭头函数、promise、import导入导出、解构赋值、扩展运算符、模版字符串

let const var区别
箭头函数和普通函数的区别
promise和ajax的区别及async和await的区别

先按照以下优先级来
1.flex、positon、BEM
2.es6：let、const、箭头函数、promise、import导入导出、解构赋值、扩展运算符、模版字符串
let const var区别
箭头函数和普通函数的区别
promise和ajax的区别及async和await的区别

CSS 盒模型
垂直水平居中
css自适应
es6常用语法有哪些
let const区别
js作用域有哪些
箭头函数和普通函数的区别
改变this指向的方式有哪些
手写防抖节流（我的博客有）
深拷贝、浅拷贝
事件循环机制
闭包
原型、原型链
https和http的区别
xss（如何预防）
csrf（如何预防）
重绘重排
打开url发生了什么
http缓存
vue2和vue3的diff算法有啥不同，还有响应式原理的不同点是什么
nextTick是什么
vuerouter的模式有哪些，底层是怎么样的（我的博客有）
vuex为啥是区分mutation为同步，不能为异步
webpack和vite的区别
git rebase和git merge的区别
git revert和git reset的区别
git flow是什么

面试

https://juejin.cn/post/7191325434486161467

博客

https://aiden124578.github.io/my_blog/
https://juejin.cn/post/7204707115062411320





**Git基础操作 创建仓库 添加   提交   推送**

### let

声明变量

```
let a
let b.c,d
let e=100;
let f=521,g='123456',h=[]

```

- #### 不能重复声明变量

var 支持变量重复声明，let 的该特性可有效防止变量命名重复、避免变量被污染。

- #### 块级作用域

块级作用域的变量仅在对应代码块内有效，出代码块后无法读取，外部调用会提示`referenceerror 变量名isnotdefined`。

var 无块级作用域，声明的变量会被添加到全局的 window 属性中，外部可正常读取。

- #### 不存在变量提升

let 无变量提升特性，**不允许在变量声明之前调用**，提前调用会直接报错，符合常规编程思维。、

var无块级作用域，声明的变量会被添加到全局的 window 属性中，外部可正常读取。

- #### 不影响作用域链

 块级作用域不会破坏 JS 的作用域链机制，若函数内部未找到某个变量，会向上一级作用域依次查找。

### const

声明常量

const shool='河南'

- #### 一定要赋初始值

const A;这是一种错误的写法

- #### 一般常量使用大写

const A=100

- #### 常量值不能修改

- #### 块级作用域

块级作用域的变量仅在对应代码块内有效，出代码块后无法读取，外部调用会提示`referenceerror 变量名isnotdefined`。

### 解构赋值

- #### 数组的解构

```js
    //数组的解构
    const F4=['张三','李四','王五','赵六']
    let [a,b,c,d]=F4
    console.log(a,b,c,d)
```

- #### 对象的解构

```javascript
    //对象的解构
    const F5={
        name:'张三',
        age:18,
        sex:'男'
        xiaopin:function(){
        console.log("我可以是你爹")
        }
    }
    let {name,age,sex}=F5
    console.log(name,age,sex)
    //这样可以 不用 F5.xiaopin
    //直接
    let{xiaopin}=F5
    xiaopin()
      
```

### 模版字符串

**``**

- #### 声明

```javascript
let str=`我也是一个字符串`
console.log(str,typeof str)
控制台输出 我也是一个字符串 sring
```

- #### 内容中可以出现换行符

```javascript
let str=`
<ul>
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
</ul>
`
可以输出
```

- #### 变量拼接

```javascript
let lovest='宋硕天'
let out=`${lovest}是我心中的帅哥`
console.log(out)

```

### 对象的简化写法

 ES6允许在大括号里面，直接写入变量和函数，作为对象的属性和方法

```javascript

    let name='宋硕天'
    let change=function(){
      console.log('我们可以变得更帅');
    }
    const school={
        name,
        change,
        //可以简化函数形式
        improve(){
        console.log("我们可以提高你的技能");
        }
    }
    
```

### 箭头函数

es6允许使用箭头=> 定义函数

声明一个函数 

```
   //箭头函数 
   let fn=(a,b)=>{
     return a+b;
   }
   let res=fn(1,2)
   console.log(res)
```

- #### this是静态的 this始终指向函数声明时所在作用域下的this的值

```javascript
  //箭头函数的this是指向全局对象的 静态的

  function fn1(){ 

  console.log(this.name);

  }

  let fn2=()=>{

  console.log(this.name);

  }

  window.name='张三'

  const shool={

  name:'zhangsan',

  }

  //直接调用

  fn1()

  fn2() //控制台输出为 张三  张三

  //call 方法调用

  fn1.call(shool)

  fn2.call(shool) //控制台输出为 zhangsan  张三
```

- #### 不能作为构造函数的实例化对象

- #### 不能使用arguments保存变量

arguments用来保存实参

- #### 箭头函数的简写

省略小括号，当形参 只有一个的时候可以省略

```javascript
 //箭头函数的简写
  //如果箭头函数只有一个参数，那么可以省略小括号
  let add=n=>{
    return n+n;
  }
  console.log(add(2))
  //如果箭头函数只有一条语句，那么可以省略大括号  
//此时return必须省略 而且语句的执行结果就是函数的返回值
  let add1=n=>n+n;
  console.log(add1(2))
```

箭头函数 适合 与this无关的回调 定时器 数组的方法回调

箭头函数不适合与this有关的回调，事件回调 对象的方法

### 函数参数默认值

- #### 形参初始值  具有默认值的参数 一般位置要靠后

```javascript
function add(a,b,c=10){
  return a+b+c；
}
let result=add(1,2)
console.log( result)
```

- #### 与解构赋值结合

```javascript
function connect({host,username,password,port}){
     console.log(host)
     console.log(username)
    console.log(password)
    console.log(port)
}

connect({
//如果没有传值 就用默认值 
host:'localhost'
username:'root
password:'root'
port:3

})
```

### rest参数

es6引入rest参数，用于获取函数的实参，用来代替arguments

- #### es5获取实参的方式

```javascript
function date(){
   console.log(arguments)
}
date ('mlxg','letme','xiaohu')  //是对象形式
```

- #### es6获取实参的方式

```javascript
function date(...args){
    console.log(args)
}
date('张三','李四','王五','赵六')//可以使用一些数组方法
//rest参数必须放在参数的最后 例如function FN(a, b, ...arg)正常，若将...arg放前面则会出错。
```

### 扩展运算算符

扩展运算符能够将数组**[  ]**转化为逗号分割的参数序列。

rest 参数声明放在函数声明的形参位置，扩展运算符放在函数调用的实参里。

```javascript
   const rng = ['张一山', '李四', '王五', '赵六']
   function lpl(){
       console.log(arguments)
   }
  lpl(...rng)   //输出结果 [] ['张一山', '李四', '王五', '赵六']
  lpl(rng)  //输出结果 [ ['张一山', '李四', '王五', '赵六']]
```

- #### rest和扩展运算符的区别

rest 参数（形参位）：打包多个参数成数组，核心是 “收集”。
扩展运算符（实参位）：拆解数组为单个参数，核心是 “展开”。

- #### 扩展运算符的应用

##### 数组的合并

```javascript
    const F4=['张三','李四','王五','赵六']
    const F5=['张一山','李四','王五','赵六']
    const F6=[...F4,...F5]
    console.log(F6)
```

##### 数组的克隆

```javascript
const F4=['张三','李四','王五','赵六']
const F5=[...F4]
console.log(F5)
```

##### 将伪数组转换为数组

```javascript
    let divs=document.querySelectorAll('div')
    console.log(divs)
    let divsArr=[...divs]
    console.log(divsArr)
```

### Symbol

- #### 创建Symbol

```javascript
let s =Symbol
console.log(s,typeof s);
```

- #### Symbol.for创建

```javascript
let s2=Symbol,for('123')
console.log(s2,typeof s2);
```

不能与其他数据进行运算

向对象中添加方法  up down

```javascript
let game={
   up:Symbol(),
   down:Symbol()
};
game[method.up]=function(){
   console.log("123456");
}
game[method.down]=function(){
   console.log("123456");
}
console.log(game);

let youxi={
    name;'狼人杀'
   [Symbol('say')]:function(){
        console.log("我可以发言")
    }
}
```

- #### Symbol.hasInstance

```javascript
//使用Symbol.hasInstance判断一个对象是否为一个类的实例
  class EvenNumber{
    static [Symbol.hasInstance](obj){
        return typeof obj === 'number' && obj % 2 === 0
    }
  }
  console.log(2 instanceof EvenNumber) // true
  console.log(3 instanceof EvenNumber) // false

```

- #### Symbol.isConcatSpreadable

```javascript
// 基础演示：默认展开数组
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];
// 默认 arr2 会展开，结果是 [1,2,3,4,5,6]
const result1 = arr1.concat(arr2);
console.log("默认展开：", result1)

//  设置 Symbol.isConcatSpreadable = false，数组不展开
arr2[Symbol.isConcatSpreadable] = false;
// 此时 arr2 作为整体被合并，结果是 [1,2,3,[4,5,6]]
const result2 = arr1.concat(arr2);
console.log("设置不展开：", result2);

```

### 迭代器

```javascript
  //使用for...of 遍历数组
  for(let item of shuihu){
    console.log(item) // 宋江 卢俊义 吴用 公孙胜
  } 
  for(let item in shuihu){
    console.log(item) // 0 1 2 3
  } 
```

### 生成器

异步编程 纯回调函数 node fs ajax mongodb

yield 是JavaScript **生成器函数 (Generator Function)** 的核心关键字

​    1.暂停 函数执行暂时停止，保存当前的上下文（变量值、执行位置）

​    2.交出 将 `yield` 后面的表达式结果返回给调用者（作为 `iterator`

`.next().value`）

​     3.等待 直到下一次调用 `next()` 方法，函数才会从 `yield` 的**下一行**继续执行。

```javascript
function * gen(){
  console.log("hello generator")
}
let iterator=gen();
iterator.next();
```

- #### 遍历

```javascript
function * gen(){
   yield’123‘
   yield’123‘
   yield’123‘
}
let iterator=gen();
console.log(iterator.next())
console.log(iterator.next())
console.log(iterator.next())
console.log(iterator.next())
```

- #### 生成器函数参数

```javascript
function * gen2(arg){
    console.log(arg)
   let one= yield 123
   console.log(one)
    let two= yield 456
    console.log(two)
    let three= yield 789
    console.log(three)
}
let iterator1=gen2('AAA');
console.log(iterator1.next())
console.log(iterator1.next('BBB'))
console.log(iterator1.next('CCC'))
console.log(iterator1.next('DDD'))
```

- #### 生成器函数解决回调地狱

```javascript
// 生成器函数的异步应用
function one(){
    setTimeout(()=>{
        console.log(111)
        ig.next()
    },1000)
}
function two(){
    setTimeout(()=>{
        console.log(222)
        ig.next()
    },2000)
}

function three(){
    setTimeout(()=>{
        console.log(333)
        ig.next()
    },3000)
}
function* generator(){
    yield one()
    yield two()
    yield three()
}
// 调用生成器函数
const ig= generator()
ig.next()
ig.next()
ig.next()

```

- #### 案例 模拟获取 用户数据 订单数据 商品数据

```javascript
//模拟获取 用户数据 订单数据 商品数据
function getUsers(){
    setTimeout(()=>{
         let data='用户数据';
         ig2.next(data)
    },1000)
}
function getOrders(){
    setTimeout(()=>{
        let data='订单数据';
        ig2.next(data)
    },1000)
}
function getProducts(){
    setTimeout(()=>{
        let data='商品数据';
        ig2.next(data)
    },1000)
}
// 模拟获取数据
function *xiaohu(){
 let users= yield getUsers()
 console.log(users)
 let orders= yield getOrders()
 console.log(orders)
 let products= yield getProducts()
 console.log(products)
}
// 调用生成器函数
const ig2= xiaohu()
ig2.next()
ig2.next()
ig2.next()
```

### promise

**异步编程内容**：主要指一些 IO 代码，包括文件 IO、数据库 IO 和网络请求。

**Promise** 是一个构造函数，可通过它实例化对象，构造函数内部用于封装异步操作，能获取成功和失败结果。

**实例化 Promise 对象时**，接受一个函数类型的参数，该函数有两个形参，一般写作 resolve 和 reject

**异步操作封装**：以定时器模拟异步操作，在异步操作中获取数据，如从数据库获取用户数据，可调用 resolve 和 reject 函数改变 Promise 对象状态。

**状态变化及结果处理**：调用 resolve 函数后，Promise 对象状态变为成功，可调用对象的 then 方法，then 方法接收两个函数类型的参数，当对象状态为成功时执行第一个回调函数；若数据读取出错，调用 reject 函数，对象状态变为失败，会执行 then 方法的第二个回调函数。

- #### promise封装读取文件

```javascript
fs.readFile('./ziyuan/ref属性.md',(err,data)=>{
    if(err){
        console.log(err)
        return
    }
    console.log(data.toString())
})

const p=new Promise((resolve,reject)=>{
    fs.readFile('./ziyuan/ref属性.md',(err,data)=>{
        if(err){
            reject(err)
            return
        }
        resolve(data)
    })
})
p.then(function(value){
    console.log(value.toString())
})
.catch(function(reason){
    console.log(reason)
})
```

- #### promise封装ajax请求

```javascript
        const p=new Promise((resolve,reject)=>{
        /* https://api.xygeng.cn/one */
        const xhr=new XMLHttpRequest()
        xhr.open('GET','https://api.xygeng.cn/one')
        xhr.send()
        xhr.onreadystatechange=function(){
            if(xhr.readyState===4){
                if(xhr.status>=200&&xhr.status<300){
                    resolve(xhr.responseText)
                }
                else{
                reject('请求失败')
            }
            }
        }
    }
)
        p.then(value=>{
            console.log(value)
        },
        reason=>{
            console.log(reason)
        }
        )
```

- #### promised的then方法

1. ##### then 方法返回结果状态

调用then方法 then方法的返回结果是promise对象，对象状态由回调函数的执行结果决定

1.如果回调函数中返回的的结果是 非promise对象 类型的属性 状态为成功 返回值为对象的成功值

2.如果回调函数返回的结果是 promise对象  promise对象的状态决定了then方法返回的promise对象的状态 对应的值也相同。

1. ##### then方法的链式调用

```javascript
        const p=new Promise((resolve,reject)=>{
            setTimeout(()=>{
                let data='获取的用户数据'
                resolve(data)
            },1000)
        })

         const obj=p.then(value=>{
            console.log(value)
            return '宋硕天'
        },
        reason=>{
            console.log(reason)
        }
        )
        console.log(obj)
        //then方法的链式调用
         p.then(value=>{

         },reason=>{
            
         }).then(value=>{
            
        },reason=>{
           
        })
```

- #### promise读取多个文件

```javascript
  //使用promise实现多个文件的读取
const p=new Promise((resolve,reject)=>{
    fs.readFile('./ziyuan/一、春行.md',(err,data)=>{
        resolve(data)
    })
})
   p.then(value=>{
      return new Promise((resolve,reject)=>{
        fs.readFile('./ziyuan/二、静夜.md',(err,data)=>{
         resolve([value,data])
        })
      })
   }).then(value=>{
      return new Promise((resolve,reject)=>{
        fs.readFile('./ziyuan/三、自勉.md',(err,data)=>{
          //push方法将data添加到value数组中
         value.push(data)
         resolve(value)
        })
      })
   }).then(value=>{
    //join方法可以将buffer数组转换为字符串 ，并在每个元素之间添加换行符
      let result=value.join('\r\n')
      console.log(result)
   })
```

- #### promise的catch方法

```javascript
  const p2=new Promise((resolve,reject)=>{
     setTimeout(()=>{
        reject('error')
     },2000)
  })
/*   p.then(function(value){
    console.log(value.toString())
  },function(reason){
     console.log(reason);
  })  
 */
p2.catch(reason=>{
    console.log(reason);
})
```

### set 集合

- #### 数组的去重

```javascript
 let s = new Set()
 let s2 = new Set(['大事儿', '小事儿', '小事儿', '好事儿 '])
 console.log(s2)
```

- #### 元素的个数

```javascript
console.log(s2,size)  //控制台输出 3
```

- #### 添加新的元素

```javascript
s2.add('喜事儿')
```

- #### 删除元素

```javascript
s2.delete('坏事儿')
console.log(s2)
```

- #### 检测

```javascript
console.log(s2.has('好事儿'));
console.log(s2);
```

- #### 清空

```
s2.clear();
```

#### Set实践

数组去重

```javascript
let s = new Set()
let s2 = new Set(['大事儿', '小事儿', '小事儿', '好事儿 '])
console.log(s2)
```

求交集

```javascript
    let arr2=[4,1,3,4,4,2,4,1,2]
    let result1=[...new Set(arr1)].filter(item=>{
        let s2=new Set(arr2);
        if(s2.has(item)){
            return true
        }else{
            return false;
        }
    })
 let  result2=[...new  Set(arr1)].filter(item=>new Set(arr2).has(item))
    console.log(result1)
    console.log(result2)

```

求并集

```javascript
 let  result3=[...new  Set(arr1)].filter(item=>!new Set(arr2).has(item))
    console.log(result3)
```

### Map

- #### 添加元素

```javascript
 let m= new Map()
 m.set('name','张三')
 m.set('age',18)
 m.set('sex','男')
 m.set('change',function(){
    console.log('我是change方法')
 })
 console.log(m)
```

- #### 删除

```
m.delete('age')
```

- #### 获取

```javascript
console.log(m.get('change'));
console.log(m.get(key));
```

- #### 清空

```javascript
m.clear()
```

- #### 遍历

```javascript
for(let item of m){
    console.log(item) 
}
```

- #### size

```javascript
console.log(m.size)
```

### class类

- #### ES5 构造函数的实例化对象

```javascript
//手机
function Phone(brand,price){
    this.brand=brand
    this.price=price
}
//添加方法 
Phone.prototype.call=function(){
    console.log('我是'+this.brand+'的手机')
}

//实例化对象
let iPhone=new Phone('苹果',8000)
iPhone.call()
console.log(iPhone);
```

- #### ES6 构造函数的实例化对象

```javascript
//class
class Phoew{
    //构造方法 名字不能修改
    constructor(brand,price){
        this.brand=brand
        this.price=price
    }
    makephone(){
        console.log('我是'+this.brand+'的手机')
    } 
}
let xiaomi=new Phoew('小米',2000)
console.log(xiaomi);
xiaomi.makephone()
```

- #### 静态成员

函数对象的属性 与 实例对象的属性 是不相通的

构造函数对象添加属性和方法

实例对象访问属性和方法

实例对象与原型对象属性相通

```javascript
class Phone{
  static name='手机'
  static change(){
    console.log('我是'+this.name+'的方法');    
  }
}
let nokia=new Phonew()
console.log(Phone.name);//控制台输出 手机
console.log(nokia.name);//控制台输出 undefined

```

**static**标注的属性 属于类  不属于实例对象

**静态成员归属**：静态成员属于类，不属于实例对象

### ES5构造函数实现继承

`call()` 是 JavaScript 中函数的内置方法，它的核心功能是：

**改变函数执行时的 `this` 指向**

**立即执行这个函数**

**可以给函数传递参数**

语法：`函数名.call(新的this指向, 参数1, 参数2, ...)`

```javascript
//构造函数实现继承
//父类
function lpl(team,player){
    this.team=team  
    this.player=player
}
lpl.prototype.jieshao=function(){
    console.log('我是'+this.team+'的'+this.player)
}
//子类
function lck(team,player,number,city){
    lpl.call(this,team,player)
    this.number=number
    this.city=city
}
lck.prototype=new Phone;
lck.prototype.constructor=lck;

lck.prototype.playGame=function(){
    console.log('我是'+this.number+'号'+this.city+'的'+this.player)
}
const lck1=new lck('SKT','FAKER',29,'韩国')
console.log(lck1);
```

```javascript
  lpl.call(this,team,player)
```

`call()` 让 `Phone` 函数**立即执行**；

call改变this指向 

this指向由 **LPL** 转到 **LCK**  

后面的**team,player**： 给LPL传递参数，让父类的属性能被初始化到子类实例上。

如果不用**call**  LPL内部的this指向 **Window** 浏览器环境/**global** Node环境

### ES6类继承

- #### 子类继承父类

```javascript
class computer{
    constructor(brand,price){
        this.brand=brand
        this.price=price
    }
    call(){
        console.log('我可以打电话');
    }
}
class SmartPhone extends computer{
    constructor(brand,price,color,size){
        super(brand,price)//Phone。call(this,brand,price)
        this.color=color,
        this.size=size
    }
    playGame(){
        console.log('我可以玩游戏');
    }
}
const huashuo=new SmartPhone('华为','5000','黑色','5.5英寸')
console.log(huashuo);
huashuo.call()
huashuo.playGame()
```

- #### 子类对父类方法的重写

```javascript
class computer{
    constructor(brand,price){
        this.brand=brand
        this.price=price
    }
    call(){
        console.log('我可以打电话');
    }
}
class SmartPhone extends computer{
    constructor(brand,price,color,size){
        super(brand,price)
        this.color=color,
        this.size=size
    }
    playGame(){
        console.log('我可以玩游戏');
    }
    //子类对父类方法的重写
    call(){
        console.log('我可以打视频电话');
    }
}
const huashuo=new SmartPhone('华为','5000','黑色','5.5英寸')
console.log(huashuo);
huashuo.call()
huashuo.playGame
```

- #### class中 getter和setter的设置

```javascript
class car{
    get price(){
        console.log('价格属性被读取了')
        return '这个价格很合适'
    }
    set price(value){
        console.log('价格属性被修改了')
    }
}
let aodi=new car()
console.log(aodi.price);
aodi.price='1000000'
```

### 数值扩展

- #### 浮点数精度问题

借助 Number.EPSILON 解决，声明函数 equal (a, b)，通过判断 Math.abs (a - b) < Number.EPSILON 来确定两数是否相等。

- #### 数值检测方法

**Number.isFinite**：用于检测一个数值是否为有限数，如 Number.isFinite (100) 结果为 true，Number.isFinite (100 / 0) 和 Number.isFinite (Infinity) 结果为 false。

**Number.isNaN**：用于检测数值是否为 NaN，在 ES6 中它作为 Number 的一个方法，方便开发者查阅文档。

**Number.isInteger**：用于判断一个数值是否为整数，如 Number.isInteger (5) 结果为 true，Number.isInteger (2.5) 结果为 false。‘

- #### **数值转换方法**

**Number.parseInt**：将字符串转化为整数，会截断浮点数，如 Number.parseInt ("5211314 love") 结果为 5211314。

**Number.parseFloat**：将字符串转化为浮点数，也会进行截取，如 Number.parseFloat ("3.1415926") 结果为 3.14。

- #### **数学处理方法**

**Math.trunc**：将数字的小数部分抹掉，如 Math.trunc (3.5) 结果为 3。

**Math.sign**：检测一个数是正数、负数还是 0，正数返回 1，0 返回 0，负数返回 -1，如 Math.sign (100) 返回 1，Math.sign (0) 返回 0，Math.sign (-20000) 返回 -1。

### 对象方法的扩展

- **Object.is 判断两个值是否完全相等**

```javascript
console.log(Object.is(100,100));//true
console.log(Object.is('a','a'));//true
console.log(Object.is({},{}));//false
console.log(Object.is(null,null));//true
console.log(Object.is(undefined,undefined));//true
```

- **Object.assign 对象的合并**

```javascript
let car1={
    brand:'奥迪',
    price:'1000000'
}
let car2={
    color:'黑色',
    size:'5.5英寸'
}
let car3=Object.assign(car1,car2)
console.log(car3);
```

- **Object.setPrototype 设置原型对象** 

```javascript
const school1={
    name:'清华大学',
}
const cities={
    xiaoqu:['清华大学','北京大学','清华大学']
}
Object.setPrototypeOf(school1,cities)
console.log(school1);
```

### es6的模块化

模块化的好处

1.防止命名冲突

2.代码复用

3.高维护性

- #### 模块化语法

**export**命令用于规定模块的对外接口

**import**命令用于输入其他模块提供的功能

```javascript
//m1.js文件
export let school='123'
export function teach(){
 console.log("我们可以是你爹")
}
```

```javascript
//index.html
//引入 m1.js 模块内容
import * as m1 from“./src/js/m1.js”
console.log(m1)
```

- #### ES6模块暴露数据

分别暴露

```javascript
//m1.js文件
//1.分别暴露
export let school='123'
export function teach(){
 console.log("我们可以是你爹")
}
```

统一暴露

```js
//m1.js文件
let school='123'
function teach(){
 console.log("我们可以是你爹")
}
//
export{school,findjob}
```

默认暴露   对象的形式

```javascript
export default{
    school:'河南师范大学'
    function teach(){
 console.log("我们可以是你爹")
}
}
```

- #### ES6模块引入数据

通用引入

```javascript
import * as m1 from“./src/js/m1.js”
```

解构赋值的形式

```javascript
import{school,teach} from "./src/js/m1.js"
import{school as guigu,findjiob} from "./src/js/m2.js"
import{default as m3} from "./src/js/m3.js"
```

简便形式 针对默认暴露

```javascript
import m3 from "./src/js/m3.js"
console.log(m3);
```

浏览器使用ES6模块化

app.js

```javascript
//入口文件
//模块引入
import * m1 from "./m1.js"
```

前端页面index.html

```javascript
<script src="./src/js/app.js" type="module"></script>
```



## Node.js、NVM、NPM、NPX 

- #### Node.js

JavaScript 的运行环境，能够编译  并执行 JavaScript 代码，让计算机可识别并运行该代码。

- #### NVM

前端生态发展快，Nodejs 更新频率高、版本多，不同版本的 Nodejs 存在兼容性问题，易导致应用在不同版本环境中无法正常运行。

nvm指令

`nvm -v` 就可以看到我们安装的nvm的版本

```arduino
nvm list available
```

查看可下载的node的版本

```
nvm install 18.20.1
```

下载node所需要的node版本

```perl
nvm use 18.20.1
```

切换node版本

```
nvm list
```

查看已下载的node版本

```
nvm uninstall 18.20.1
```

卸载node版本

- #### NPM

无 NPM 时，使用第三方库需手动下载代码、放置并通过 script 标签引入，项目复杂时，第三方库依赖关系繁琐，手动管理难度极大；NPM 可通过简单命令自动下载所需第三方库及所有依赖，管理依赖关系，也能轻松删除无用的库。

- #### NPX

NPM 会将依赖包安装到本地项目 node_modules 文件夹或全局环境；NPX 可在不安装全局包的情况下执行本地 / 远程仓库中的包。

执行命令时，先在项目 node_modules 文件夹中查找目标包，找到则直接执行；未找到则从网络临时下载包到内存，执行完成后立即删除，无任何残留。

## Flex 布局

- #### 快速实现一个元素的 水平垂直居中

```javascript
display：flex
justify-content：center
align-items：center
```

**align-items**：控制每一行内部flex项目在交叉轴上的对齐

​                flex-start（交叉轴起点）、flex-end（交叉轴终点）、center（交叉轴中心）等值。

**align-content**：控制所有行作为一个整体在交叉轴上的对齐

flex-start：向起始边靠拢

flex-end：向结束边靠拢

space-between	第一行贴顶，最后一行贴底，中间的行均匀分布。

space-around	每行的上下都有相等的间距（看起来行间距是边缘间距的2倍）。

space-evenly	所有间距（包括边缘和行之间）完全相等。

- #### 完美居中网格布局

```javascript
justify-content;center
align-items:center
align-content:center
```

flex-shrink 可以阻止 container里的项目的收缩

flex-shrink：0 不可以被压缩

flex-shrink：1 可以被压缩   

 flex-wrap: wrap; 用于控制当弹性盒子（flex items）在一行中无法全部容纳时，是否允许它们换行。

flex-grow：1 flex项目会填满父容器内的可用空间

flex-grow：0 flex项目不会填满父容器内的可用空间

align-self：flex-end 对单个flex项目进行操作 覆盖掉父容器设置的 `align-items` 属性。

## position定位

position 可选值：有 static、relative、absolute、fixed 和 sticky。

absolute 绝对定位：只要存在 position 值是四个定位之一，子元素就会以它为参照物进行定位

## Vue3

### 核心逻辑

```javascript
// 1. 从 Vue 核心库中导入 createApp 函数
import { createApp } from 'vue'

// 2. 导入根组件 App（通常是 App.vue），这是整个应用的根容器
import App from './App.vue'

// 3. 核心逻辑：创建应用实例 + 挂载到 DOM 节点
// createApp(App)：基于根组件 App 创建一个 Vue 应用实例
// .mount('#app')：将应用实例挂载到页面中 id 为 "app" 的 DOM 元素上
createApp(App).mount('#app') 
```

### 创建方法

- #### 使用vue-cli创建

```cmd
//查看@vue/cli版本
vue--version
//安装或者升级vue/cli
npm install -g @vue/cli
//创建
vue create vue_test
//启动
cd vue_test
npm run serve
```

- #### 使用vite创建  

无需打包操作 可快速冷启动

```cmd
//创建工程
npm init vite-app <project-name>
//进入工程目录
cd <project-name>
//安装依赖
npm install
//运行
npm run dev
```

- ####   分析vue3 工程结构 vue-cli创建的

###  Set up

- **数据配置**：

在 Vue3 中不用再写 data 配置项，直接定义变量即可，如 last name = ' 张三 '，age = 18 ，不使用 const 是因为数据可能会改变。

- **方法配置**：

直接写函数，如 function sayHello () { alert (`我叫${name}，我${age}岁了，你好！`); } ，在 setup 函数内可直接访问变量，无需使用 this

- **set up 的两种返回值** 

1.若返回一个对象，其对象中的属性，方法  在模版中都可以直接使用

2.若返回一个渲染函数，则可以自定义渲染内容

- **Vue2和Vue3的配置 不要混用**

```javascript
export default {
  name: 'App',
//Vue2方法
  data() {
    return {
      xingming: '宋硕天',
      age: 18
    }
  }, 
  methods: {
    sayWelcome() {
      alert(`欢迎${this.xingming}来到vue2世界`)
    }
  },
 //Vue3方法
  setup() {
     let name='vue组件'
     let age=18
     //方法
     function sayHello(){
        alert(`我是${name},我今年${age}岁`)
     }
     return{
      name,
      age ,
      sayHello
     }
  }
}
```

- **setup 函数注意事项**

**不能为 async 函数**：async 函数返回值会被 Promise 包裹，模板中的数据将无法使用，写代码时要避免因使用 await 而错误添加 async。

### ref函数 

作用:定义一个响应式的数据

语法:

```javascript
const xxx=ref{initValue}
```

js中操作数据：xxx.value

模版中读取数据：不需要value，直接<div>{{xxx}}</div>



- #### Vue2 与 Vue3 的 ref 对比

**Vue2 的 ref 属性**：是标签属性，用于给元素打标识，类似原生 JS 里 ID 的替代者，可用于获取元素并进行操作，如让元素获取焦点。

**Vue3 的 ref 函数**：是新增的函数，原来的 ref 属性依然可用。

- #### **引入 ref 函数的背景**：

**数据响应式问题**：在 Vue3 中直接定义普通的字符串和数字数据，修改时 Vue 无法监测到，页面不会更新，因为这些数据不是响应式数据。

**解决方案**：引入 ref 函数，将普通数据交给 ref 函数加工，使其变成能被 Vue 监测到的响应式数据。

```javascript
import { ref } from 'vue'
export default {
  name: 'App',
  setup() {
     let name=ref('vue组件')
     let age=ref(18)
     function changeName(){
      name.value='新的姓名' 
      age.value=20  
     }
     return{
      name,
      age 
      ,changeName
     }
  }
}
```

- #### **ref 函数的使用方法**：

**加工数据**：把正常配置的数据交给 ref 函数，如原本直接写 “张三” 和 “18”，现在改为 ref (“张三”) 和 ref (18)。

**读取和修改数据**：ref 加工后的数据是一个对象，读取和修改数据需要通过.value 属性，读时走 get，改时调 set，set 里封装了更新页面的逻辑。

- #### **ref 函数实现响应式的原理**：

**与 Vue2 对比**：Vue2 通过 Object.defineProperty 配合 getter 和 setter 实现数据响应式，Vue3 的 ref 函数同样借助 Object.defineProperty 和 getter、setter 实现响应式。

**隐藏机制**：Vue3 中 getter 和 setter 藏在原型对象里，这样使数据展示更干净，且当查找属性时会自动查找原型对象。

**类比理解**：ref 加工后的数据类似 Vue2 里的_data，将值放在 value 属性中，为方便取用又将其放在外层，如同把_data 里的属性放在 vm 身上。

**编码关注要点**：编码时关注是否点 value，原则是取出 ref 传入的东西点 value，后续继续取东西不用点 value。

### reactive函数

作用:定义一个对象类型的响应式(基本数据类型不要用它，要用ref函数)

- #### **reactive 基本使用**

语法：

```
const 代理对象=reactive(源对象)
```

接收一个对象(或数组)，返回一个代理对象(proxy)对象

reactive定义的响应式数据是"深层次的"。

内部基于ES6的proxy实现，通过代理对象操作源对象内部数据进行操作

- **reactive 基本使用**

**避免基本类型**：

reactive 不能处理基本类型数据，传入基本类型无法将其变为响应式

**处理对象类型**：

可将对象类型数据用 reactive 定义成响应式对象，如将之前定义的 “工作” 对象用 reactive 定义，此时读取和修改数据无需点 value。

- **reactive 对象特性**

**proxy 实例**：

reactive 处理后的对象输出为 proxy 实例对象，而非普通 object 对象，目的是将数据变为响应式，使 Vue3 能检测到对象属性的修改并更新页面

**深层响应式**：

reactive 处理对象类型数据时是深层次的，即使对象嵌套层次很深，修改深层属性也能被监测到

- **处理数组类型数据**：

**普通数组问题**：

直接定义数组，通过索引修改数据可能无法生效。

**响应式处理**：

使用 reactive 将数组变为响应式后，可直接通过索引读取和修改数据，且在 Vue3 中可行，与 Vue2 不同

- **reactive 与 ref 对比**

**适用范围**：

ref 可处理基本类型和对象类型，处理对象类型时借助 reactive；reactive 只能处理对象或数组类型。

**使用便捷性**：

**在script中**

ref 定义响应式数据需频繁点 value，代码繁琐且不美观；reactive 无需点 value，代码更简洁、语义化。

### Vue2 响应式核心原理

用 `Object.defineProperty()` 劫持对象的属性，在`get`中收集依赖（Watcher），在`set`中触发依赖更新；

```javascript
    //模拟vue2的响应式原理
    let person={
        name:'vue组件',
        age:18,
    }
    let p={}
    Object.defineProperty(p,'name',{
        get(){
            console.log('name属性被读取了')
            return person.name
        },
        set(newValue){
            console.log('name属性被修改了')
            person.name=newValue
        }
    })

    Object.defineProperty(p,'age',{
        get(){
            console.log('age属性被读取了')
            return person.age
        },
        set(newValue){
            console.log('age属性被修改了')
            person.age=newValue
        }
    }) 

```



### Vue.3.0中的响应式原理-proxy

- #### 实现原理 


**通过proxy**：拦截对象中任意属性的变化，包括：属性值的读写.属性的添加.属性的删除等

**通过Reflect**：对源对象的属性进行操作

```javascript
const p=new Proxy(person,{
    //有人读取p的某个属性时调用
    get(target,prop){
        console.log('name属性被读取了')
        return target[prop]
    },
    //set不仅修改的时候调用 增加的时候也调用
    set(target,prop,newValue){
        console.log('name属性被修改了')
        //target[prop] 是方括号语法，不是数组形式，核心作用是支持变量作为属性名
        //点语法（target.prop）只能访问「固定名称」的属性，无法识别变量；//在 Proxy 的 get 拦截器中，prop 是动态传入的属性名变量，因此必须用方括号语法才能正确读取目标对象的对应属性。
        target[prop]=newValue
    } 
    //删除的时候调用
       deleteProperty(target,prop){
        console.log(`${prop}属性被删除了`)
        return delete target[prop]
    }
})
```

**认识`Proxy`**：`Proxy`是`window`身上的内置构造函数，用于实现代理。它能让代理对象映射对原对象的操作，且能监测到操作变化。

**`Proxy`语法**：创建`Proxy`实例时需要传入两个参数，第一个参数是要代理的对象，第二个参数是配置对象，若不想配置可传入空对象占位。

**配置`get`和`set`**：在配置对象中编写`get`和`set`方法。`get`方法能收到`target`（原对象）和`property`（读取的属性名）两个参数，可根据这些参数返回正确的值；`set`方法除了`target`和`property`，还能收到修改的值`value`。

### Vue.3.0中的响应式原理-Reflect

```javascript
const p=new Proxy(person,{
    //有人读取p的某个属性时调用
    get(target,prop){
        console.log('name属性被读取了')
        return Reflect.get(target,propName)
    },
    //set不仅修改的时候调用 增加的时候也调用
    set(target,prop,newValue){
        console.log('name属性被修改了')
        //target[prop] 是方括号语法，不是数组形式，核心作用是支持变量作为属性名
        //点语法（target.prop）只能访问「固定名称」的属性，无法识别变量；//在 Proxy 的 get 拦截器中，prop 是动态传入的属性名变量，因此必须用方括号语法才能正确读取目标对象的对应属性。
        target[prop]=newValue
        Reflect.set(target,propName,value)
    } 
    //删除的时候调用
       deleteProperty(target,prop){
        console.log(`${prop}属性被删除了`)
        return  Reflect.deleteProperty(target,propName)
    }
})
```

### reactive对比ref

**ref用来定义**：基本数据类型

**reactive用来定义**：对象或者数组

**备注：**ref可以用来定义对象(或数组) 它内部会自动通过reactive转为代理对象

**ref**通过**Object.defineProperty()**的get与set来实现响应式

**reactive**通过使用proxy来实现响应式，并通过Reflect操作源对象内部的数据

**ref定义数据**需要   **. value**        读取数据时模版中直接读取不需要.value

**reactive定义的数据** 操作数据与读取数据 都不需要  **.value**

### setup的两个注意点

- #### setup执行的时机

在beforeCreated之前执行一次 this是undefined

- #### setup参数

**props**：

​         值为对象，包含：组件外部传递过来，且组件内部声明接受了的属性

 **context**：上下文对象

​        **context.emit :向父组件 传递数据，并类似于接受数据props一样要声明方法，如emits:['hello']**

​       分发自定义事件的函数, 相当于 ```this.$emit```。

​        **context.attrs :与vue2一样拿props不要的数据**

​        值为对象，包含：组件外部传递过来，但没有在props配置中声明的属性, 相当于 ```this.$attrs```。

​        **context.slots :插槽语法**    （vue2使用v-slot="名字",vue3使用v-slot:名字）

​      收到的插槽内容, 相当于 ```this.$slots```。

**子组件**

```javascript
 <script>
 import { reactive ,ref } from 'vue'
 export default{
   name:'Demo',
   props:['msg'],
   emits:['hello'],
   setup(props,context){
     console.log(props)
     //attrs拿props没有接受的数据
     console.log(context.attrs)
     // emit触发事件  相当于Vue2的$emit
     console.log(context.emit)
      //收到的插槽内容, 相当于 ```this.$slots```
    console.log(context.slots)
     let person=reactive({
        name:'汤东信',
        age:'21'
     })
     let sex=ref('男')
     console.log(person)
     console.log(sex);
     function test(){
        context.emit('hello','我是子组件')
     }
     return{
       person,
       sex,
       test
     }
   }
 }
 </script>
```

**父组件：**

```javascript
<template>
    
  <Demo @hello="showMsg" msg="person">
      <span>RNG</span>
   </Demo>
//v-slot:插槽id
   <template v-slot:qwe>
       <span>RNG</span>
   </template>  
</template>
<script>
import Demo from "./components/Demo.vue";
export default {
  name: "App",
  components: {
    Demo,
  },
  setup() {
    function showMsg(msg) {
      console.log(`子组件触发了hello事件，传递的参数是：${msg}`);
    }
    return {
      showMsg,
    };
  },
};
</script>
```

### 计算属性与监视

- #### computed函数   

  与Vue2.x中computed配置功能一致

  写法

```javascript
import {computed} from 'vue'
setup(){
    ...
	//计算属性——简写
    let fullName = computed(()=>{
        //return 暴露出去
        return person.firstName + '-' + person.lastName
    })
    //计算属性——完整
    let fullName = computed({
        get(){
            return person.firstName + '-' + person.lastName
        },
        set(value){
            //将一个字符串 value 按照分隔符 - 拆分成数组，并赋值给 nameArr
            const nameArr = value.split('-')
            person.firstName = nameArr[0]
            person.lastName = nameArr[1]
        }
    })
}
```

- #####  watch函数

  监视reactive定义的响应式数据时：oldValue无法正确获取、强制开启了深度监视（deep配置失效）。

  监视reactive定义的响应式数据中某个属性时：deep配置有效。

  **immediate:true**：立即开始监听   

```javascript
//情况一：监视ref定义的响应式数据
watch(sum,(newValue,oldValue)=>{
	console.log('sum变化了',newValue,oldValue)
},{immediate:true})

//情况二：监视多个ref定义的响应式数据
watch([sum,msg],(newValue,oldValue)=>{
	console.log('sum或msg变化了',newValue,oldValue)
}) 

/* 情况三：监视reactive定义的响应式数据
			若watch监视的是reactive定义的响应式数据，则无法正确获得oldValue！！
			若watch监视的是reactive定义的响应式数据，则强制开启了深度监视 
*/

//最常用的是这个
watch(person,(newValue,oldValue)=>{
	console.log('person变化了',newValue,oldValue)
},{immediate:true,deep:false}) //此处的deep配置不再奏效

//情况四：监视reactive定义的响应式数据中的某个属性
watch(()=>person.job,(newValue,oldValue)=>{
	console.log('person的job变化了',newValue,oldValue)
},{immediate:true,deep:true}) 

//情况五：监视reactive定义的响应式数据中的某些属性
watch([()=>person.job,()=>person.name],(newValue,oldValue)=>{
	console.log('person的job变化了',newValue,oldValue)
},{immediate:true,deep:true})

//特殊情况
watch(()=>person.job,(newValue,oldValue)=>{
    console.log('person的job变化了',newValue,oldValue)
},{deep:true}) //此处由于监视的是reactive所定义的对象中的某个属性，所以deep配置有效
```

### watch的value问题

```javascript
import {ref,watch} from 'vue'
 export default{
    name:'Demo',
    setup(){
      let sum=ref(0)
      let person=ref('hello')
      let game=ref({
        name:'LOL',
        phone:'13800000000',
        job:{
          type:'前端开发',
          company:'字节跳动'
        }
      })
      //第一种解决方法 开始深度监听
      watch(game,(newVal,oldVal)=>{
        console.log(newVal,oldVal)
      },{deep:true})
       //第二种解决方法 添加 .value
      watch(game.value,(newVal,oldVal)=>{
        console.log(newVal,oldVal)
      })
     return{
       sum,
       person,
       game
     }
    }
 }
```

**监视基本类型数据（sum）**：

**不点value**：直接写sum进行监视，sum变化时能收到new value 和old value 并输出，可正常监测。

**点 value**：点 value 后报错，因把真正的值（如 0）取出，不能直接监测值，而应监测保存数据的结构，点 value 后功能无法实现。

**监视对象类型数据（game）**：

**不点 value**：直接写 game 监视，修改game 信息时监测不到变化。原因是game是 REF 生成的对象，其 value 是 reactive 生成的代理对象，只改 value 里子对象的值，代理对象在内存中的地址不变，认为值未变化。

**点 value**：点 value 后监视的是 reactive 所定义的数据，其特点是深层次且自动开启深度监视，能解决监测问题。

**不点 value 的另一种办法：**可通过开启深度监视来进一步判断 proxy 实例对象里的内容变化，从而解决监测问题。

### watch的Effect函数

watch的套路是：既要指明监视的属性，也要指明监视的回调。

watchEffect的套路是：不用指明监视哪个属性，监视的回调中用到哪个属性，那就监视哪个属性。

watchEffect有点像computed：

1.    但computed注重的计算出来的值（回调函数的返回值），所以必须要写返回值

2.    而watchEffect更注重的是过程（回调函数的函数体），所以不用写返回值。

```javascript
//watchEffect所指定的回调中用到的数据只要发生变化，则直接重新执行回调。
watchEffect(()=>{
    const x1 = sum.value
    const x2 = person.age
    console.log('watchEffect配置的回调执行了')
})
```

### Vue3的生命周期

![image-20260311005711136](C:\Users\22974\AppData\Roaming\Typora\typora-user-images\image-20260311005711136.png)

Vue3.0也提供了 Composition API 形式的生命周期钩子，与Vue2.x中钩子对应关系如下：

beforeCreate`===>`setup()` 

`created`=======>`setup()` 

beforeMount` ===>`onBeforeMount`  组件挂载到 DOM 之前执行

mounted`=======>`onMounted`          组件挂载到 DOM 之后执行

beforeUpdate`===>`onBeforeUpdate`  响应式数据更新、DOM 重新渲染前

updated` =======>`onUpdated` 响应式数据更新、DOM 重新渲染后

beforeUnmount` ==>`onBeforeUnmount` 组件卸载之前执行

unmounted` =====>`onUnmounted` 组件卸载完成后执行

Vue3.0中可以继续使用Vue2.x中的生命周期钩子，但有有两个被更名：

`beforeDestroy```改名为 ```beforeUnmount

```destroyed```改名为 ```unmounted

### 自定义hook函数

什么是hook？—— 本质是一个函数，把setup函数中使用的Composition API进行了封装。

类似于vue2.x中的mixin。

自定义hook的优势: 复用代码, 让setup中的逻辑更清楚易懂。

### toRef

创建一个 ref 对象，其value值指向另一个对象中的某个属性。

```javascript
const name = toRef(person,'name')
```

要将响应式对象中的某个属性单独提供给外部使用时。

```toRefs``` 与```toRef```功能一致，但可以批量创建多个 ref 对象，语法：

```javascript
toRefs(person)
```

- #### 必须配合扩展运算符：单独写 toRefs(person) 会返回一个普通对象，模板无法直接访问其属性，必须用 ... 展开。

```javascript
 ...toRefs(person),
```



###  shallowReactive 与 shallowRef

 shallowReactive：只处理对象最外层属性的响应式（浅响应式）。

shallowRef：只处理基本数据类型的响应式, 不进行对象的响应式处理。

什么时候使用?

1. 如果有一个对象数据，结构比较深, 但变化时只是外层属性变化 ===> shallowReactive。

2. 一个对象数据，后续功能不会修改该对象中的属性，而是生新的对象来替换 ===> shallowRef。

### readonly 与 shallowReadonly

readonly: 让一个响应式数据变为只读的（深只读）。

shallowReadonly：让一个响应式数据变为只读的（浅只读）。

应用场景: 不希望数据被修改时。 

```javascript
import { reactive, ref, toRefs ,readonly} from "vue";
export default {
  name: "Demo",
  setup() {
    let sum = ref(0);
    let person = reactive({
      name: "张三",
      age: 18,
      sex: "男",
      job: {
        type: "前端开发",
        salary: "3000",
      },
    });
   person = readonly(person);
    return {
      sum,
      ...toRefs(person),
    };
  },
};
```

### toRaw 与 markRaw

- **toRaw作用**：将一个由```reactive```生成的<strong style="color:orange">响应式对象</strong>转为<strong style="color:orange">普通对象</strong>。

  ```javascript
  const ptoRaw(person)
  ```

使用场景：用于读取响应式对象对应的普通对象，对这个普通对象的所有操作，不会引起页面更新。

- **markRaw作用**：标记一个对象，使其永远不会再成为响应式对象。

  ```javascript
  person.car=markRaw(car)
  ```

1. 有些值不应被设置为响应式的，例如复杂的第三方类库等。
2. 当渲染具有不可变数据源的大列表时，跳过响应式转换可以提高性能。

### customRef

创建一个自定义的 ref，并对其依赖项跟踪和更新触发进行显式控制

```javascript
  import {customRef} from 'vue'
  export default {
    name: "App",
    setup(){
      /* let keyWord=ref("hello")  */ //使用Vue内部的ref
      let timer
       function myRef(value,delay){
          return customRef((track,trigger)=>{
            return {
              get(){
                console.log(`有人读取了keyWord,我把${value}返回给你`);
                  //通知Vue追踪keyWord的变化
                track();
                return value;
              },
              set(newValue){
                console.log(`有人修改了keyWord,我把${newValue}记录在册`);
                value=newValue;
                clearTimeout(timer);
                timer=setTimeout(()=>{
                  trigger();
                },delay)
              }
            }
          })
       }
      let keyWord=myRef("hello",500)  //使用Vue内部的ref
      return{
        keyWord,
        myRef
      }
    } 
  }
```

执行流程：初始化时 `get` 触发 `track()` 建立依赖 → 修改时 `set` 触发 `trigger()` 通知更新 → 重新渲染时再次 `get` 返回新值。

### provide 与inject

 作用：实现<strong style="color:#DD5145">祖与后代组件间</strong>通信

套路：父组件有一个 `provide` 选项来提供数据，后代组件有一个 `inject` 选项来开始使用这些数据

具体写法:

1.父组件

```javascript
setup(){
	......
    let car = reactive({name:'奔驰',price:'40万'})
    provide('car',car)
    ......
}
```

2. 后代组件中

```javascript
setup(props,context){
	......
    const car = inject('car')
    return {car}
	......
}
```

### 响应式数据的判断

- isRef: 检查一个值是否为一个 ref 对象
- isReactive: 检查一个对象是否是由 `reactive` 创建的响应式代理
- isReadonly: 检查一个对象是否是由 `readonly` 创建的只读代理
- isProxy: 检查一个对象是否是由 `reactive` 或者 `readonly` 方法创建的代理

### Composition API 的优势

-  **定义**：基于 setup 语法糖（Vue3 推荐），按 “业务逻辑” 组织代码，核心是把同一个功能的代码（数据、方法、监听等）聚合在一起。

- **特点**：逻辑复用性极强（比如抽离通用的 “分页逻辑”“表单校验逻辑”），复杂组件的代码结构更清晰，支持 TypeScript 友好。

### Teleport

什么是Teleport？—— `Teleport` 是一种能够将我们的<strong style="color:#DD5145">组件html结构</strong>移动到指定位置的技术。

父组件

```javascript
<template>
    <div class="Son">
      <h3>
          我是Son组件 孙组件
          姓名：{{name }}   年龄：{{age }}
        <Dialog></Dialog>
      </h3>
    </div>
  </template>
  <script>
  import Dialog from './Dialog.vue'
  import { inject,toRefs } from 'vue';
  export default{
    name:"Son",
    components:{
      Dialog,
    },
    setup(){
      let person = inject('person');
      return{
        ...toRefs(person),
      }
    }
  }
  </script>
  <style>
  .Son{
     background-color: rgb(123, 105, 255);
     padding: 20px;
  }
  </style>
```

子组件

```javascript
<template>
  <div>
    <button @click="dialogShow = true">打开弹窗</button>
    <teleport to="body">
      <div v-if="dialogShow" class="mask">
        <div class="Dialog">
          <h3>我是一个弹窗</h3>
          <h4>一些内容</h4>
          <h4>一些内容</h4>
          <h4>一些内容</h4>
          <h4>一些内容</h4>
          <button @click="dialogShow = false">关闭弹窗</button>
        </div>
      </div>
    </teleport>
  </div>
</template>
<script>
import { ref } from "vue";
export default {
  name: "Dialog",
  setup() {
    let dialogShow = ref(false);
    return {
      dialogShow,
    };
  },
};
</script>
<style>
.mask {
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.5);
}
.Dialog {
  text-align: center;
  position: absolute;
  transform: translate(-50%, -50%);
  top: 50%;
  left: 50%;
  background-color: rgba(255, 196, 0, 0.603);
  width: 300px;
  padding: 20px;
}
</style>

```

 

### **suspense**

等待异步组件时渲染一些额外内容，让应用有更好的用户体验

使用步骤

```javascript
import {defineAsyncComponent} from 'vue'
const Child = defineAsyncComponent(()=>import('./components/Child.vue'))
```

使用```Suspense```包裹组件，并配置好```default``` 与 ```fallback

<template>
	<div class="app">
		<h3>我是App组件</h3>
		<Suspense>
			<template v-slot:default>
				<Child/>
			</template>
			<template v-slot:fallback>
				<h3>加载中.....</h3>
			</template>
		</Suspense>
	</div>
</template>

可以配合async 和await函数使用

```javascript
<template>
  <div class="App">
     <Suspense>
      <template v-slot:default>
        <Child></Child>
      </template>
      <template v-slot:fallback>
        <div>加载中...</div>
      </template>
    </Suspense>
  </div>
</template>
<script>
import { reactive, toRefs,provide } from 'vue';
import { defineAsyncComponent } from 'vue';
const Child = defineAsyncComponent(() => import('./components/Child.vue'));
export default{
  name:"App",
  components:{
    Child,
  },
  setup(){
    let person = reactive({
      name:"张三",
      age:18,
    });
    provide('person',person);
    return{
      ...toRefs(person),
    }
  } ,
  async setup(){
     let p=new Promise((resolve,reject)=>{
      setTimeout(()=>{
        resolve();
      },2000);
    })
    return await p
  }
}
</script>
```

