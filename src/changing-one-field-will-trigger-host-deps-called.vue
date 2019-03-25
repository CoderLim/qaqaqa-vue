<!--
  1、只修改name，不会触发host的依赖执行回调
  2、如果修改host，则name和addr直接与原来的值做比较，如果一致，则不触发依赖的回调函数
  3、如果是给host新增field，host的Dep回调也会执行；
	                       host下的基本数据类型不会触发依赖回调；
												 host下的复杂类型也会触发依赖回调；
		 IMPORTANT: 如果想测试这种情况，必须保证host内的数据在template中都用到了，
		 因为vue的动态依赖收集策略，如果没用到就不存在dep回调触发的逻辑
												 
  如果是给vuex的$store.state设置新属性，那state下的所有属性都会被通知
	这个是幻觉，请参考上面的第3点;

	ps: 新增field指的是通过$set方法
-->
<template>
  <div>
    {{host.name}}
    <br>
    {{host.addr}}
		<ul>
			<li v-for="t of host.childList" :key="t">{{ t }}</li>
		</ul>
    <button @click="btnOnClick">change host</button>
    <button @click="changeNameBtnOnClick">change host.name</button>
    <button @click="addNewFieldOnClick">add new field to `host</button>
  </div>
</template>

<script>
let counter = 1;
export default {
  data() {
    return {
      host: {
        name: 'host_name',
        addr: 'host_addr',
        childList: [ 1, 2, 3,4,5, ],
      },
    };
  },
  methods: {
     btnOnClick() {
       this.host = {
        name: 'host_name',
        addr: 'new addr',
       };
     },
     changeNameBtnOnClick() {
       this.host.name = counter++;
     },
     addNewFieldOnClick() {
       // 这种方式添加新属性是不响应的
       // this.host.newField = counter++;;

       this.$set(this.host, 'newField', 'xxx');
     },
  },
  watch: {
    host() {
      console.log('host changed');
    },
    'host.name'() {
      console.log('host.name changed');
    },
    'host.childList'() {
      console.log('complicated child notified');
    },
  },
  mounted() {
    window.temp = this;
  },
}
</script>
