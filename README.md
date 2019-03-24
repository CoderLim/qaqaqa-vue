
## 一些关于 vue 的小疑问

### 计算属性不能用箭头函数

### v-on=“$listeners”, v-bind="$attrs", v-model="xxx"

### $children 不是响应式的

### 如何防止 select 数据变化

### 同一事件循环中，对 group 多次赋值，只有第一次会触发 render，但是 group 的值是最后一次赋值的

### 同一循环中，如果多次对 group 赋值，那依赖于 group 的计算属性会多次计算吗？

### template 可以有多个根元素

### HOC 怎么搞

### v-once/keep-alive/functional

### 利用 props 解耦 $router

### 接口请求应该在哪个生命周期

### 边界情况 $store $router 建议不要直接用

### 生命周期前几步是同步执行的？

### v-if vs v-show

### v-if keep-alive 如何实现的

### require.context 批量注册组件，省的每次都要手动添加到 components 中

### vue 有没有静态方法

### css 的 class 会直接传递给组件的根元素

### 所有的计算属性是在同一事件循环中处理的吗

### 自定义组件支持 v-model

### 28、联动
区域
CN —> [信息流，小游戏]
US —> [信息流us]
初始设置 region为us，group为[信息流]，group肯定展示的是空，如果修改region为cn，group也不会更新展示

### 29、记一次状态管理的坑

### 29、计算属性的循环引用

### 30、 计算属性与watch的本质
