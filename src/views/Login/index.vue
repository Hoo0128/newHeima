<template>
  <div>
    <van-nav-bar
      class="navbar"
      title="登录"
      left-text
      left-arrow
      @click-left="onClickLeft"
    >
      <template #left>  <van-icon name="cross" /> </template>
    </van-nav-bar>
  </div>
</template>

<script>
import { Toast } from 'vant'
export default {
  methods: {
    onClickLeft () {
      Toast('返回')
    }
  }
}
</script>

<style lang="less" scoped>
.navbar {
  background-color: #3296fa;
  :deep(.van-nav-bar__title) {
    color: #fff;
  }
  .van-icon {
    color: #fff;
  }
}
</style>
