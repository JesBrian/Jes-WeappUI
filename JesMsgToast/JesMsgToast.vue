<template>
    <view v-if="status && value" class="jes-class jes-msg-toast" >
      <jes-icon-font v-if="icon" class="icon" :icon="icon" size="33" />
      <text class="message">{{ value }}</text>
      <jes-icon-font @click="switchEvent(false)" class="closeBtn" icon="iconLogonClosed" size="33" />
    </view>
</template>

<script lang="ts">
	import Vue from 'vue';

	export default Vue.extend({
		name: "JesMsgToast",

		props: {
		  icon: {
		    type: String,
        default: ''
      },
		  value: {
		    type: String,
        default: ''
      },
      closeBtn: {
		    type: Boolean,
        default: true
      },
      duration: {
		    type: Number,
        default: 5000
      }
		},

		data(): any {
			return {
        status: true,
        nowDuration: this.duration
			}
		},

    watch: {
		  status: {
		    handler(nVal: boolean, oVal: boolean): void {
		      if (nVal) {
		        this.$nextTick().then(() => {
		          if (this.duration > 0) this.timer = setInterval(() => {
                this.nowDuration -= 200;
                if (this.nowDuration <= 0) {
                  this.switchEvent(false);
                  this.nowDuration = this.duration;
                }
              }, 200);
            });
          } else {
            this.timer && clearInterval(this.timer);
            this.nowDuration = this.duration;
          }
        },
        immediate: true
      }
    },

    beforeDestroy(): void {
      this.timer && clearInterval(this.timer);
    },

    methods: {
      switchEvent(status: boolean): void {
        this.status = (typeof status === 'undefined' ? !this.status : status);
        if (!this.status) {
          this.status = true;
          this.$emit('input', '');
        }
      }
		}
	});
</script>

<style lang="scss" scoped>
    @import "JesMsgToast.scss";
</style>
