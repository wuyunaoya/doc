# 一.vuex

## 1.定义

Vuex 是一个专为 Vue.js 应用程序开发的**状态管理模式**，采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化

## 2.安装

```
npm i vuex --save
```

## 3.使用

1.获取状态管理层的数据

```
$store.state.属性名
```

2.修改状态管理层的数据

```js
两种方式:
方式一:
	在组件中
	<!-- 1.通过commit提交到mutations中修改状态
         2.传递多个值时使用json
     -->
    <button @click="$store.commit('changeName','杨幂')">杨幂</button>
    
    在main.js
    // 专门状态数据的修改
      mutations:{
        changeName(state,aa){
          state.name = aa;
        },
        changeAge(state,age){
          state.age = age
        }
      },
          
 方式二:
	在组件中
    	 <!--
          1.dispatch跟actions进行对接
         -->
        <button @click="$store.dispatch('ageActions',40)">40</button>
	在main.js
		//对接dispatch进行提交到actions
          actions:{
            ageActions(context,age){
              context.commit('changeAge',age)
            }
          }
```

```
总结:
	1.state:专门做状态数据的获取
	2.mutations:专门状态数据的修改,  通过commit提交对接mutaions
	3.actions:专门做对接mutaions,通过dispatch 对接actions,在action中commit到mutations
```

3.优化在组件中获取状态层的数据和修改

```
1.获取状态层的数据
	// 1.mapGetters和mapActions在vuex中内置的变量
    // 2.mapGetters对接状态层的getters
    // 3.mapActions对接状态层的actions
    import {mapGetters} from 'vuex';
        computed:{
        // 在计算属性接收mapGetters
        ...mapGetters({
          "name1":"newName",
          "age":"age"
        })

      },
      
      在main.js中的状态层通过getters返回state中的数据
        // 将state中的属性返回到组件中
          getters:{
            newName(state){
              return state.newName
            },
            age(state){
              return state.age
            }
          }
 2.修改状态层的数据
 		// 1.mapGetters和mapActions在vuex中内置的变量
        // 2.mapGetters对接状态层的getters
        // 3.mapActions对接状态层的actions
        import {mapActions} from 'vuex';
    
    	methods:{
            ...mapActions({
              "changeName":"nameActions"
            }),
            // changeName(name){

            // }
          },
          
         在main.js 中对接actions
          //对接dispatch进行提交到actions
          actions:{
            nameActions(context,name){
              context.commit('changeName',name)
            },
            ageActions(context,age){
              context.commit('changeAge',age)
            }
          },
```

```
总结:
1.store中有5个选项:state mutations actions getters modules
2.state:专门做状态的数据获取
3.mutations:通过commit提交到mutaions中修改状态层的数据
4.actions:通过dispatch对接actions,最后commit到mutations,修改状态层的数据
5.getters:返回state中的数据,对接mapGetters
		1.要使用mapGetters,首先需要引入:import {mapGetters} from  'vuex'
		2.在computed中使用mapGetters
			computed:{
				...mapGetters({
					//选项eg
					"组件中要展示变量名":"getters中对应的函数名"
				})
			}
6.actions:对接mapActions
		  1.要使用mapActions,首先需要引入:import {mapActions} from  'vuex'
		  2.在methods中使用mapActions
		  		methods:{
		  			...mapActions({
		  				//选项
		  				"组件中调用的函数名":"actions中对应的函数名
		  			})
		  		}
7.modules:{}存放的是模块中的每一个选项,namespaced:true
	在组件中使用时:
	computed:{
		...mapGetters({
			"显示在页面中的变量":"命名空间名称/对应getters中的方法"
		})
	}
```

```js
原生写法: 在main.js
// 引入vuex
// import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

const store = new Vuex.Store({
  // 专门做存放数据
  state:{
    newName:'王俊凯',
    age:20
  },
  // 专门状态数据的修改
  mutations:{
    changeName(state,aa){
      state.newName = aa;
    },
    changeAge(state,age){
      state.age = age
    }
  },
  //对接dispatch进行提交到actions
  actions:{
    nameActions(context,name){
      context.commit('changeName',name)
    },
    ageActions(context,age){
      context.commit('changeAge',age)
    }
  },
  // 将state中的属性返回到组件中
  getters:{
    newName(state){
      return state.newName
    },
    age(state){
      return state.age
    }
  }
})

/* eslint-disable no-new */
new Vue({
  el: '#app',
  components: { App },
  template: '<App/>',
  // 状态管理
  store
})
```

```js
封装:
src/store/index.js
	import Vue from 'vue'
    import Vuex from 'vuex'

    Vue.use(Vuex)

    import {state,mutations,getters} from './mutations';
    import actions from './actions';

    export default new Vuex.Store({
      // 专门做存放数据
      state,
      // 专门状态数据的修改
      mutations,
      //对接dispatch进行提交到actions
      actions,
      // 将state中的属性返回到组件中
      getters
    })
src/store/mutations.js
	export const state = {
          newName:'王俊凯',
            age:20
        };
    export const mutations = {
        changeName(state,aa){
            state.newName = aa;
        },
        changeAge(state,age){
            state.age = age
        }
    };
    export const getters = {
        newName(state){
            return state.newName
        },
        age(state){
            return state.age
        }
    }
    
src/store/actions.js
	export default {
      nameActions(context,name){
        context.commit('changeName',name)
      },
      ageActions(context,age){
        context.commit('changeAge',age)
      }
    }

```



# 二.elementUI

## 1.安装

```
npm i element-ui -save
```

```js
在main.js中引入
import Vue from 'vue';
import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';

Vue.use(ElementUI);
```

