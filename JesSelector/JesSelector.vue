<template>
  <view class="jes-class jes-selector" :class="selecting?'selecting':''">
    <view @click="selecting = !selecting" :class="['showContainer', checkIndex < 0 ? 'placeholder' : '']">
      {{checkIndex > -1 ? source[checkIndex].label : placeholder}}
      <view class="triangle"/>
    </view>
    <view v-if="source.length" v-show="selecting" class="selectContainer">
      <view v-for="(selectItem, index) in source" @click="selectItem(index)" class="selectItem">
        {{selectItem.label}}
      </view>
    </view>
    <view v-show="selecting" @click="selecting = !selecting" class="cloverContainer" ></view>
  </view>
</template>

<script lang="ts">
  import Vue from 'vue';

  export default Vue.extend({
    name: 'JesSelector',

    props: {
      placeholder: {
        type: String,
        default: ''
      },

      checked: {
        type: String,
        default: ''
      },

      source: {
        type: Array,
        default: () => []
      }
    },

    data(): any {
      return {
        selecting: false,
        checkIndex: -1,
      }
    },

    watch: {
      checked: {
        handler(nVal: boolean, oVal: boolean): void {
          for (let i = 0, len = this.source.length; i < len; i++) {
            if (this.source[i].key === nVal && this.checkIndex !== i) {
              this.checkIndex = i;
              break;
            }
          }
        },
        immediate: true
      }
    },

    methods: {
      selectItem(index: number = -1): void {
        this.checkIndex = index;
        this.selecting = false;
        this.$emit('', {
          index,
          item: this.source[index]
        });
      },

      switchSelectStatus(status: boolean = true): void {
      }
    }
  });
</script>

<style lang="scss" scoped>
  @import 'JesSelector.scss';
</style>
