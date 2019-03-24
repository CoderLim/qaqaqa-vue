
<template>
  <div>
    <h1>{{ key1 }}</h1>
    <button @click="btnOnClick">点击</button>
  </div>
</template>

<script>
export default {
  data () {
    return {
      key1: 'data',
    };
  },
  methods: {
    btnOnClick () {
      this.key1 = 'data1';
      this.key1 = 'data2';
    },
  },
  mounted () {
    console.log(this);
  },
}
</script>
