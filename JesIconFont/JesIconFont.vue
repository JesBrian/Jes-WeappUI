<template>
  <text @click="click" :class="'iconfont ' + icon" :style="'font-size:' + size + 'rpx;' + (color ? ('color:' + color + ';') : '')"/>
</template>

<script lang="ts">
  import Vue from 'vue';

  export default Vue.extend({
    name: "JesIconFont",

    props: {
      icon: {
        type: String,
        default: '',
      },
      size: {
        type: String | Number,
        default: 30
      },
      color: {
        type: String,
        default: ''
      }
    },

    methods: {
      click () {
        this.$emit('click');
      }
    }
  });
</script>

<style lang="scss" scoped >
  @import 'JesIconFont.scss';
</style>
