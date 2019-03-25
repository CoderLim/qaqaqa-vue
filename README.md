
## Prerequisite

1. Install vue-cli;
2. yarn global add @vue/cli-service-global

## Run

vue serve {file}

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
现象：点击时间轴后，分组select变成了all

1. 查看groupsInSelectedRegion(computed)，依赖与groups和formData.region；
2. 使用watch看到：groups有变化和formData.region无变化；
3. groups是直接保存在vuex的store里的，通过接口获取的数据，经查看内容发现groups并没有修改；
4. groups内容没变，难道groups被clone重新赋值的？
5. 通过查看vue的devtool发现，点击时间轴后，触发了两次Action：MOUNTED
6. 经多打断点发现是Jimu里的action，难道是积木修改了vuex的store？打印store.state发现确实多了一个jimu这个变量；
7. 但是通过代码没发现clone数据再赋值的，但是发现jimu这个变量是$set；
8. 试一下直接temp.$set(temp.$store.state, 'new1', 'value1'), 确实state下的变量都被通知了；
9. 然后试了一下普通变量temp.$set(temp.formData.test, 'new1', 'value1'), 发现formData的子数据没被通知，那么问题就是vuex了，当添加新属性时，会通知所有子数据；
10. 但是看过vuex的代码后没发现有这逻辑，经过几次尝试，发现添加新属性时，只有非基本数据类型的变量才会被通知，wtf！

### 29、计算属性的循环引用

### 30、 计算属性与watch的本质

### 31、如何创建shadow对象，也就是只对obj设置reactive，不对其子节点设置
