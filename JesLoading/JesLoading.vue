<template>
  <view v-if="visible" class="jes-class jes-loading">
    <view class="icon"/>
    <text class="label">{{isLoading ? loadingLabel : loadendLabel}}</text>
  </view>
</template>

<script lang="ts">
  import Vue from 'vue';

  export default Vue.extend({
    name: "JesLoading",

    props: {
      visible: {
        type: Boolean,
        default: true
      },
      isLoading: {
        type: Boolean,
        default: true
      },
      loadingLabel: {
        type: String,
        default: '加载中 ···'
      },
      loadendLabel: {
        type: String,
        default: '加载完成'
      }
    },

    data(): any {
      return {}
    },

    methods: {}
  });
</script>

<style lang="scss" scoped>
  @import "JesLoading.scss";
</style>
