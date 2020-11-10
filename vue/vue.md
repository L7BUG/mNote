# vue

- # 循环判断
    - `if else`
    - `for`

- # 属性
    - ## `el`
    - ## `data`
    - ## `methods`
    - ## `computed` (计算属性)
- # 组件 `Vue.component`
    - `props` 组件属性 不能大写
    - `template` 定义的模板
- # Axios 异步通信
    ```  
    data() {
            return {
                info: {}
            },
            mounted() {
                // 钩子函数 ajax请求
                axios.get('../data.json').then(response => (this.info = response.data));
            }
    }
    ```
- # 计算属性(类似缓存)
    - 该属性里面的方法只会调用一次 再次调用会直接给**缓存中的结果**， 除非**方法中的数据更新** 类似**缓存**
- # 插槽 `slot`
    1. `name` 插槽name
    2. `slot` 属性  绑定一个slot
- # 自定义事件
    - 组件上写 `v-on` 即可自定义事件
    - this.$emit('事件名'); //触发事件
- # webpack `打包工具`
    - ## entry 主入口
    - ## output 
        - 打包输出路径
- # vue-cli
> *官方提供脚手架*
    
    1. vue init webpack myvue
    2. cd myvue
    3. npm install
    4. npm run dev
- # vue-router 路由
    1. npm install vue-router --save-dev
    2. ```
        import Vue from 'vue';
        import VueRouter from "vue-router";
        // 安装路由
        Vue.use(VueRouter);
        ```
    3. 导入组件
        ```
        import Content from "../components/Content";
        ```
    4. 配置组件
        ```
        export default new VueRouter({
                routes: [
                  {
                    // 路由路径
                    path: '/content',
                    // 路由名称
                    name: 'content',
                    // 跳转的组件
                    component: Content
                  }
                ]
          }
        );
        ```
    5. `main.js` 中引用路由
        ```
        import router from './router'
        new Vue({
            el:'#app',
            router
        })
        ```
    6. 使用路由
        ```
            <router-link to="/content">内容页</router-link>
            <router-view></router-view>
        ```
    > 嵌套路由
    - children
- # element ui