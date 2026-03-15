## ref属性

1.被用来给元素或子组件注册引用信息(id的替代者)2.应用在html标签上获取的是真实DoM元素，应用在组件标签上是组件实例对象(vc)3.使用方式:
打标识:<h1 ref="xxx">.....</h1>或<School ref="xxx"></School>

获取 this.$refs.xxx





## 配置项props

功能:让组件接收外部传过来的数据
(1).传递数据:
<Demo name="xxx"/>
(2).接收数据:
第一种方式(只接收):
props:['name']
第二种方式(限制类型):
props:{
name:Number
 }
第三种方式(限制类型、限制必要性、指定默认值):

props:{name:
type:String,//类型
required:true,//必要性

default:'老王'//默认值

 }

备注:props是只读的，Vue底层会监测你对props的修改，如果进行了修改，就会发出警告，若业务需求确实需要修改，那么请复制props的内容到data中一份，然后去修改data中的数据



## mixin(混入)

功能:可以把多个组件共用的配置提取成一个混入对象使用方式:
第一步定义混合，例如:
{

data(){....}

methods:{

.....

}

}
data(){....}methods:{....}
}
第二步使用混入，例如:
(1).全局混入:Vue.mixin(xxx)

(2).局部混入:mixins:['xxx']





## 插件

功能:用于增强Vue
本质:包含install方法的一个对象，install的第一个参数是Vue，第二个以后的参数是插件使用者传递的数
据。
定义插件:
对象.install = function (Vue, options) {
//1.添加全局过滤器
Vue.filter(....)
//2.添加全局指令
Vue.directive(....)
//3.配置全局混入(合)
Vue.mixin(....)
//4.添加实例方法
Vue.prototype.$myMethod = function () {...}
Vue.prototype.$myProperty = xxxx
}
使用插件:Vue.use()





## scoped样式

作用:让样式在局部生效，防止冲突。
写法:<style scoped>



## 总结TodoList案例

1.组件化编码流程:(1).拆分静态组件:组件要按照功能点拆分，命名不要与html元素冲突。(2).实现动态组件:考虑好数据的存放位置，数据是一个组件在用，还是一些组件在用:
1).一个组件在用:放在组件自身即可。
2).一些组件在用:放在他们共同的父组件上(状态提升)。
(3).实现交互:从绑定事件开始。
2.props适用于:
(1).父组件==>子组件通信
(2).子组件==>父组件通信(要求父先给子一个函数)
3.使用v-model时要切记:v-model绑定的值不能是props传过来的值,因为是不可以修改的!
4.props传过来的若是对象类型的值，修改对象中的属性时Vue不会报错，但不推荐这样做





## webStorage

1.存储内容大小一般支持5MB左右(不同浏览器可能还不一样)
2.浏览器端通过Window.sessionStorage和 Window.localStorage属性来实现本地在储机制.
3.相关API:

1. xxxxxStorage.setItem('key', 'value');
     该方法接受一个键和值作为参数，会把键值对添加到存储中，如果键名存在，则更新其对应的值。
2. xxxxxStorage.getItem('person');该方法接受一个键名作为参数，返回键名对应的值。
3. xxxxxStorage.removeItem('key');该方法接受一个键名作为参数，并把该键名从存储中删除。
4. xxxxxStorage.clear()
     该方法会清空存储中的所有数据。
       4.备注:
       1.SessionStorage存储的内容会随着浏览器窗口关闭而消失。
       2.LocalStorage存储的内容，需要手动清除才会消失。
5. xxxxxstorage.getItem(xxx)如果xxx对应的value获取不到，那么getltem的返回值是null。
     英
6. JSON.parse(null)的结果依然是null。





## 组件的自定义事件

1.一种组件间通信的方式，适用于:子组件===>父组件
2.使用场景:A是父组件，B是子组件，B想给A传数据，那么就要在A中给B绑定自定义事件(事件的回调在A中)。
3.绑定自定义事件:
1.第一种方式，在父组件中:<Demo @atguigu="test"/>或 <Demo v-on:atguigu="test"/>
2.第二种方式，在父组件中:
<Demo ref="demo"/>
mounted(){
this.$$refs.xxx.$on('atguigu',this.test)

 }

3.若想让自定义事件只能触发一次，可以使用once修饰符，或$once方法。
js
英，品
4.触发自定义事件:this.$emit('atguigu',数据)
5.解绑自定义事件this.$off('atguigu')
6.组件上也可以绑定原生DOM事件，需要使用native修饰符。
7.注意:通过 this.$refs.xxx.son' atguigu',回调)绑定自定义事件时，回调要么配置在methods中，要么用箭头函数，否则this指向会出问题!



## 全局事件总线

1.组件间的通信的方式 适用于任意组件间通信

2.安装全局事件总线

```javascript
new Vue({
  ......
  beforeCreate(){
    Vue.prorotype.$bus=this //安装全局事件总线
  }，
  ....
  
})
```

3.使用事件总线

​     1.接收数据:A组件想接收数据，则在A组件中给$bus绑定自定义事件，事件的回调留在A组件自身。   

```javascript
methods(){
demo(data)......
 }
mounted() {
this.$bus.$on('xxxx',this.demo)
  }
```


​    2.提供数据: 

```
this.$bus.$emit('xxxx'，数据)
```

4.最好在beforeDestroy钩子中，用$off去解绑当前组件所用到的事件

## 消息订阅与发布(pubsub)

1.一种组件间通信的方式，适用于任意组件间通信。
2.使用步骤:
1.安装pubsub:

```
npm i pubsub-js
```


2.引入:

```javascript
import pubsub from 'pubsub-js'
```

3.接收数据:A组件想接收数据，则在A组件中订阅消息，订阅的回调留在A组件自身。

```javascript
methods(){
demo(data){......}
}
mounted() {
this.pid = pubsub.subscribe('xxx',this.demo)
]//订阅消息.
```


4.提供数据:

```javascript
pubsub.publish('xxx',数据)
```

5.最好在beforeDestroy钩子中,用

```javascript
Pubsub.unsubscribe(pid)
```

去取消订阅。

## nextTick

1.语法

```javascript
this.$nextTick
```

(回调函数)
2.作用:在下一次DOM更新结束后执行其指定的回调。
3.什么时候用:当改变数据后，要基于更新后的新DOM进行某些操作时，要在nextTick所指定的回调函数中执行。



## Vue封装的过度与动画

写法：

1.准备好样式:

​     元素进入的样式

​              1.v-enter 进入的起点

​             2.v-enter-active 进入过程中

​           3.v-enter-to 进入的终点

​            元素离开的样式

​             1.v-leave:离开的起点
​            2.v-leave-active:离开过程中

​                 3.v-leave-to:离开的终点

2.使用<transition>包裹要过度的元素，并配置name属性:

```javascript
<transition name="hello">
   <h1 v-show="isShow">hello 汤东信</h1>
</transition>
```

3.备注:若有多个元素需要过度，则需要使用:<transition-group>，且每个元素都要指定key值。

## 插槽

1.作用：让父组件可以向子组件指定位置插入html结构，也是一种组件间通信的方式，适用于父组件===>子组件

2.分类:默认 具名 作用域
3.使用方式：
​    1.默认插槽

```javascript
父组件中：
   <Category title="游戏">
    <div>html结构1</div>
   </Category>
子组件中
<template>
  <div class="category">
    <slot>如果没有内容 这里展示默认内容</slot>
  </div>
</template>
```

​    2.具名插槽

```javascript
父组件中：
<Category>
  <template slot="center">
  <div>html结构1</div>
  </template>
  
  <template v-slot="footer">
  <div>html结构2</div>
  </template>
</Category>
子组件中：
<template v-slot="footer">
  <div>
<slot name="center">插槽默认内容。。。</slot>
<slot name="footer">插槽默认内容。。。</slot>
</div>
</template>

```

   3.作用域插槽
​     1.理解:数据在组件的自身，但根据数据生成的结构需要组件的使用者来决定。(games数据在Category组件中，但使用数据所遍历出来的结构由App组件决定)
2.

```javascript
父组件  
 <Category title="游戏">
     <template scope="songshuotian">
      <ul>
        <li v-for="(g,index) in songshuotian.youxi" :key="index">{{g}}</li>
      </ul>
     </template>
   </Category>
   <Category title="游戏">
     <template scope="songshuotian">
      <ol>
        <li v-for="(g,index) in songshuotian.youxi" :key="index">{{g}}</li>
      </ol>
     </template>
   </Category>
   <Category title="游戏">
     <template slot-scope="youxi">
      <h4 v-for="(g,index) in youxi" :key="index">{{g}}</h4>
     </template>  
   </Category>
子组件
<template>
  <div class="category">
    <h3>{{title}}</h3>
    <slot :youxi="games">如果没有内容 这里展示默认内容</slot>
  </div>
</template>
<script>
    export default{
        name:'Category',
        props:['title'],
        data(){
            return{
                games:['生化危机:安魂曲','王者荣耀世界','宝可梦传说Z-A','影之刃零'],  
            }
        }
    }
</script>j
```

## Vuexj

### 搭建环境

#### 1.创建文件  src/store/index.js

```javascript
//该文件用于 创建vuex中最为核心的store
import Vuex from 'vuex'
import Vue from 'vue'
//使用vuex插件
Vue.use(Vuex)
//准备actions用于响应组件中的动作
const actions = {}
//准备mutations用于操作数据(state)
const mutations = {}
//准备state用于存储数据
const state = {}
//创建并导出store
export default new Vuex.Store({
    actions,
    mutations,
    state
})  

```

#### 2.在main.js中创建vm时传入store配置项

```javascript
import Vue from 'vue'
import App from './App.vue'
//引入vue-resource插件
import  vueResource from 'vue-resource'
//引入store
import store from './store/index.js'

Vue.config.productionTip = false // 阻止 vue 在启动时生成生产提示
// 安装插件 先安装插件 再创建vue实例 
Vue.use(vueResource)
new Vue({
    store,
    el:"#App",
    render:h=>h(App),
    beforeCreate(){
        //在beforeCreated中，将当前实例赋值给Vue.prototype.$bus
        //在生命周期钩子中  this指向当前实例vm
        Vue.prototype.$bus= this //安装全局事件总线
    }
})

```

### 基本使用

#### 1.初始化数据,配置 actions 配置 mutations 操作文件 store.js

```javascript
//该文件用于 创建vuex中最为核心的store
import Vuex from 'vuex'
import Vue from 'vue'
//使用vuex插件
Vue.use(Vuex)
//准备actions用于响应组件中的动作
const actions = {
/*     //响应组件中的动作
    increment(context,value){
        context.commit('increment',value);
    },
    //响应组件中的动作
    decrement(context,value){
        context.commit('decrement',value);
    }, */
    //响应组件中的动作
    incrementodd(context,value){
        if(context.state.count % 2 !== 0){
            context.commit('JIA',value);
        } 
    },
    //响应组件中的动作
    addtwait(context,value){
        console.log('action addtwait');
        setTimeout(()=>{
            context.commit('JIA',value);
        },3000);
    }
}
//准备mutations用于操作数据(state)
const mutations = {
    //响应actions中的动作
    JIA(state,value){
        state.count += value;
    },
    //响应actions中的动作
    JIAN(state,value){
        state.count -= value;
    },
}
//准备state用于存储数据
const state = {
    count:0,//当前的和初始化状态
}
//创建并导出store
export default new Vuex.Store({
    actions,
    mutations,
    state
})  

```

#### 2.组件中读取vuex中的数据：

```javascript
$store.state.sum
```

#### 3.组件中修改vuex中的数据：

```javascript
$store.dispatch('actions中的方法名'，数据)或者$store.commit('mutations中的方法名字'，数据)
```

备注 若没有网络请求或其他业务逻辑，组件中也可以越过actions，即不写dispatch，直接编写commit

#### 5.getters的使用

###### 1.概念：当state中的数据需要经过加工后再使用时，可以使用getters加工

###### 2.在store.js中追加getters配置

```javascript
//准备getters用于将state中的数据进行加工
const getters = {
    //提供一个方法 可以返回当前的和
    bigSum(state){
        return state.count*10
    }
}
//创建并导出store
export default new Vuex.Store({
..,
..,
..,
gettersj
})  
```

###### 3.组件中读取数据：

```javascript
$store.getters.bigSum
```

#### 6.四个map方法的使用

##### 1.mapState方法 ：用于帮助我们映射state中的数据为计算属性

```javascript
//使用mapState映射sum,school,subject到计算属性中 对象方法          ...mapState({he:'sum',xuexiao:'school',xueke:'subject'})
//使用mapState映射sum,school,subject到计算属性中 数组方法 数组里面的对象必须是 state 中的属性
...mapState(['sum','school','subject']),
```

##### 2.mapGetters方法：用于帮助我们映射getters中的数据为计算属性

```javascript
//使用mapGetters映射bigSum到计算属性中 数组写法
...mapGetters(['bigSum']),
//使用mapGetters映射bigSum到计算属性中 对象写法
...mapGetters([bigSum:'bigSum']),
```

##### 3.mapActions方法：用于借助我们生成后的action对话的方法 即包含$store.dispatch(xxx)的函数

```javascript
// 方法中会调用commit去联系mutation 对象方法
...mapMutations({increment:'JIA',decrement:'JIAN'}),
// 方法中会调用dispatch去联系action 数组方法
...mapActions(['incrementodd','addtwait']),
```

##### 4.mapMutations方法：用于帮助我们生成与mutation对话的方法 即包含$store.commit(xxx)的函数

```javascript
//对象方法         ...mapActions({incrementodd:'incrementodd',addtwait:'addtwait'}),
//数组方法
...mapActions(['incrementodd','addtwait'])
```

#### 7.模块化+命名空间

##### 1.目的：让代码更好维护，让多种数据分类更加明确

##### 2.修改store.js

```javascript
export default{
    //开启命名空间
    namespaced:true,
    actions:{
        incrementodd(context,value){
            if(context.state.count % 2 !== 0){
                context.commit('JIA',value);
            } 
        },
        //响应组件中的动作
        addtwait(context,value){
            console.log('action addtwait');
            setTimeout(()=>{
                context.commit('JIA',value);
            },3000);
        },
    },
    mutations:{
        JIA(state,value){
            state.count += value;
        },
        //响应actions中的动作
        JIAN(state,value){
            state.count -= value;
        }, 
    },
    state:{
        count:0,//当前的和初始化状态
        school:'河南师范大学',
        subject:'前端',
    },
    getters:{
        //提供一个方法 可以返回当前的和
        bigSum(state){
            return state.count*10
        }
    }
}


//创建并导出store
export default new Vuex.Store({
   modules:{
    countAbout:countOption,
    personAbout:personOption,
   }
})  

```

##### 3.开启命名空间后，组件读取state的数据

```javascript
//直接读取
return this.$store.state.school;
//借助mapState读取
...mapState('countAbout',['count','school','subject'])
```

##### 4.开启命名空间后，组件读取getters的数据

```javascript
自己读取
this.$store.dispatch('personAbout/ADD_PERSON',person)
借助mapActions
...mapActions('countAbout'{incrementodd:'incrementodd',addtwait:'addtwait'})
```

##### 5.开启命名空间后，组件中调用dispatch

```javascript
自己调用
this.$store.dispatch('',person)
借助mapActions
...mapActions('countAbout'{incrementodd:'incrementodd',addtwait:'addtwait'}),
```

##### 6.开启命名空间后，组件中调用commit

```javascript
自己直接commit
this.$store.commit('personAbout/ADD_PERSON',personObj);
借助mapMutations
...mapActions('countAbout',{incrementodd:'incrementodd',addtwait:'addtwait'}),
```

## 路由的使用

### 1.基本使用

1.安装vue-router，命令 npm i vue-router

2.应用插件: Vue.use(Vue Router)

3.编写router 配置项

```javascript
import VueRouter from `vue-router`
import About from `../components/About`
import Home from `../components/Home`
const router =new VueRouter({
  routes:[
    {
      path:'/about'
      component:About
    },
    {
      path:'/home'
      component:Home
    }
  ]
})
export dafault router
```

4.实现切换

<router-link active-class="active" to="/about">About</router-link>

5.指定展示位置

<router-view></router-view>

### 2.几个注意

1.路由组件在pages里面 一般组件在components文件夹

2.通过切换，“隐藏”了的路由，默认是被销毁的，需要的时候再去挂载

3.每个组件都有自己的$route属性，里面存储自己的的路由信息

4.整个应用只有一个router，可以通过组件的$router属性获取到

### 3.多级路由

1.配置路由规则，使用children配置项：

```javascript
    routes:[
        {
            path:'/Home',
            component:Home,
            children:[
                {
                    path:'Me',
                    component:Me,
                },
                {
                    path:'User',
                    component:User,
                },
            ]
        },
        
        {
            path:'/Profile',
            component:Profile,
        },
        {
            path:'/Messages',
            component:Messages,
        },
    ]
```

2.跳转(填写完整路径)

```javascript
 <li><router-link role="presentation" class="active" to="/Home/Me">个人中心</router-link></li>
```

### 4.路由的query参数



### 5.命名路由

#### 1.作用：可以简化路由的跳转

#### 2.如何使用

##### 1.给路由命名：

```javascript
const router = new VueRouter({
    routes:[
        {
            name:'guanyu',
            path:'/Home',
            component:Home,
            children:[
                {
                    name:'wode',
                    path:'Me',
                    component:Me,
                    children:[
                        {
                            name:'xiangqing',
                            path:'Detail',
                            component:Detail,
                        },
                    ]
                },
                {
                    name:'yonghu',
                    path:'User',
                    component:User,
                },
            ]
        },
        
        {
            path:'/Profile',
            component:Profile,
        },
        {
            path:'/Messages',
            component:Messages,
        },
    ]
})
```

##### 2.简化跳转

```javascript
简化
<router-link role="presentation" :to="{name:'yonghu'}">用户</router-link>
```

### 6.路由的params参数

#### 1.配置路由，声明接收params参数

```javascript
const router = new VueRouter({
    routes:[
        {
            name:'guanyu',
            path:'/Home',
            component:Home,
            children:[
                {
                    name:'wode',
                    path:'Me',
                    component:Me,
                    children:[
                        {
                            name:'xiangqing',
                            path:'Detail/:id/:title',
                            component:Detail,
                        },
                    ]
                },
                {
                    name:'yonghu',
                    path:'User',
                    component:User,
                },
            ]
        },
        
        {
            path:'/Profile',
            component:Profile,
        },
        {
            path:'/Messages',
            component:Messages,
        },
    ]
})
```



#### 2.传递参数

```javascript
<router-link 
:to="{name:'xiangqing',params:{id:item.id,title:item.title}}">
 {{item.title}}
</router-link>
```

特别注意：路由携带params参数时，若使用to的对象写法，则不能使用path配置项

必须使用name配置

#### 3.接收参数：

```javascript
$route.params.id
$route.params.title
```

### 7.路由的props配置

作用：让路由组件更方便的收到参数

```javascript
{
  name:'xiangqing',
  path:'detail/:id',
  component:Detail,
  第一种写法：props值为对象，该对象中所有的key-value的组合最终都会通过props传给Detail组件
  props：{a:900}
  第二种写法：props值为布尔值，布尔值为true 则把路由收到的所有params参数通过props传给Detail组件
  props：true
  第三种写法：props值为函数，该函数返回的对象中每一组key-value都会通过props传给Detail组件
  props(route){
    return{
      id：route.query.id,
      title:route.query.title
    }
  }
}
```

### 8.<route-link>的replace属性

1.作用：控制路由跳转时操作浏览器历史记录的模式

2.浏览器的历史记录有两种写入方式：分别为 push和replace push是追加 历史记录 replace是替换当前记录，路由跳转时候默认为push

3.如何开启 replace模式： <router-link replace......>news<router-link>

### 9.编程式导航

1.作用：不借助<router-link>实现路由跳转，让路由跳转更灵活

2.具体编码

```javascript
//$router的两个api
this.$router.push({
  name:'xiangqing'
   params：{
     id:xxx,
     title:xxx
   }
})
this.$router.replace({
name:'xiangqing'
 params:{
   id:xxx,
   title:xxx
 }
})
this.$router.forward()
this.$router.back()
this.$router.go(3)

```

### 10.缓存路由组件

1.作用：让不展示的路由组件保持挂载，不被销毁。

2.具体编码

```javascript
<keep-alive include="User">
<router-view></router-view>
</keep-alive>

```

### 11.两个新的生命周期钩子

1.作用:路由组件所独有的两个钩子，用于捕获路由组件的激活状态

2.具体名字：

1.activated 路由组件被激活时触发

2.deactivated 路由组件失活时触发

### 12.路由守卫

1.作用：对路由进行权限控制

2.分类：全局守卫，独享守卫 组件内守卫

#### 3.全局守卫

```javascript
//全局前置守卫 初始化的时候被调用 每次路由切换之前被调用
router.beforeEach((to,from,next)=>{
    if(to.meta.isAuth){ //判断是否需要权限
        //如果需要权限，就判断是否是学校用户
        if(localStorage.getItem('school')==='1'){
            //如果是学校用户，就放行
            next()
        }
        //如果不是学校用户，就提示不能访问
        else{
            alert('您不是学校用户，不能访问')
        }
    }
    //如果不需要权限，就放行
    else{ 
        next()
    }
})
//全局后置守卫  初始化的时候被调用 每次路由切换之后被调用
router.afterEach((to,from)=>{
    if(to.meta.title){
        //如果路由元信息中存在标题，就设置标题为路由元信息中的标题
        document.title=to.meta.title
    }else{
        //如果路由元信息中不存在标题，就设置标题为默认标题
        document.title='默认标题'
    }
})
```

#### 4.独享守卫

```javascript
beforeEnter(to,from,next){
        if(localStorage.getItem('school')==='1'){
         next()
         }else{
         alert('您不是学校用户，不能访问')
          }
    },

```

#### 5.组件内路由守卫

```javascript
        //通过路由规则，进入该组件时被调用
        beforeRouteEnter(to,from,next){
            console.log('Home-beforeRouteEnter',to,from);
        if(to.meta.isAuth){ //判断是否需要权限
        //如果需要权限，就判断是否是学校用户
        if(localStorage.getItem('school')==='1'){
            //如果是学校用户，就放行
            next()
        }
        //如果不是学校用户，就提示不能访问
        else{
            alert('您不是学校用户，不能访问')
        }
        }
        else{
            next()
        }
        },
        //通过路由规则，离开该组件时被调用
        beforeRouteLeave(to,from,next){
          console.log('Home-beforeRouteLeave',to,from);
          
        } 
    }
```

### 13.路由器的两种工作模式

1.对于一个url来说，什么是hash值？—#及其后面的内容就是hash值

2.hash值不会包含在http请求中，即：hash值不会带给服务器

3.hash模式

​    1.地址中永远带着#号，不美观

​    2.若以后将地址通过第三方手机app分享，若app校验严格，则地址会被标记为不合法

​    3.兼容性好

4.history模式 

   1.地址干净美观

   2.兼容性和hash模式相比略差

   3.应用部署上线时需要后端人员支持，解决刷新页面服务端404的问题