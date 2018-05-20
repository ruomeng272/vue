vue中使用vuex
1.下载vuex npm install vuex -D
2.与src平级新建store文件夹
3.store文件夹中新建index.js
4. index.js中内容：
    import Vue from 'vue'
    import Vuex from 'vuex'
    Vue.use(Vuex)
  const store = new Vuex.Store({
      state: { // 全局数据（所有定义的数据变量）
        num: 0,
        obj: {
            name: '张三',
            age: 13
        }
      },
      actions: {
          change_num ({commit}) {
              commit('changeNum')
          },
          change_obj({commit}, obj){
              commit('changeObj', obj)
          }
      },
      mutations: {
          changeNum(state, num){
              state.num ++;
          },
          changeObj(state,obj){
              state.obj.name = '李四'
              state.obj.age = 18
          }
      },
      getters: {

      }
  })


5.在main.js中引入store  并挂载到vue实例上
    import store from './store'
    new Vue({
        el: '#app',
        router,
        store,
        components: { App },
        template: '<App/>'
    })
6. 在组件中使用
import {mapActions, mapSate} from 'vuex'
在methods中写：
    methods:{
        ...mapActions(['change_num', 'change_obj', 'change_server',]) //对应的是store中actions中的方法

    }
在computed中写：
computed:{
    ...mapState(['num', 'obj', 'server']) // 对应的是store中state中定义的变量
}
在html中写：
<p>{{num}}</p>
<p>{{name}}</p>
<p>{{age}}</p>
<button @click="changeOne">改变num</button>
<button @click="changeTwo">改变obj</button>
