<template>
  <div>
      <div class="demo demo-hook" ref='demoHook'>
        123acd
      </div>
  </div>
</template>

<script type="text/ecmascript">
  // export default 和 export的区别
// import {hotcss} from './assets/hotcss/hotcss';
 
  export default {
    data () {
      return {
        data1: 1
      };
    },
    beforeCreate () {
      console.log(1);
      
    },
    created () {
      console.log(2);
      
    },
    beforeMount () {
      console.log(3);
      
    },
    mounted () {
      let oDiv = this.$refs.demoHook;
      oDiv.innerHTML = this.data1;
      console.log(oDiv);
      console.log(4);
    },
    beforeUpdate () {
      console.log(5);
    },
    updated () {
      let oDiv = this.$refs.demoHook;
      console.log(oDiv);
      console.log(6);
    },
    beforeDestroy () {
      console.log(7);
    },
    destroyed () {
      this.data1 = '';
      console.log(8);
      
    }
  };
</script>

<style lang="scss" scoped>
  @import '../assets/hotcss/px2rem.scss';

</style>
