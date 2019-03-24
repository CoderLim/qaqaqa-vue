<!--
  只修改name，不会触发host的依赖执行回调
  如果修改host，则name和addr直接与原来的值做比较，如果一致，则不触发依赖的回调函数
  如果是给host新增field，则host的watch也会执行；
  如果是给vuex的$store.state设置新属性，那state下的所有属性都会被通知
-->
<template>
  <div>
    {{host.name}}
    <br>
    {{host.addr}}
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
        childHost: {
          field1: 'value1',
          field2: 'value1',
        },
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
    'host.newField'() {
      console.log('newField changed');
    },
  },
  mounted() {
    window.temp = this;
  },
}
</script>
