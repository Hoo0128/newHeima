<template>
  <div>
    <van-nav-bar class="navbar" title="账号登录" @click-left="onClickLeft">
      <template #left> <van-icon name="arrow-left" />  </template>
    </van-nav-bar>

    <van-form @submit="onSubmit">
      <van-field
        v-model="mobile"
        name="mobile"
        placeholder="请输入账号"
        :rules="[{ required: true, message: '请输入账号' }]"
      >
        <template #label>
          <span></span>
        </template>
      </van-field>

      <van-field
        v-model="code"
        type="password"
        name="code"
        placeholder="请输入密码"
        :rules="[{ required: true, message: '请输密码' }]"
      >
        <template #label>
          <span></span>
        </template>

      </van-field>

      <div style="margin: 16px">
        <van-button block type="info" native-type="submit">登录</van-button>
      </div>
    </van-form>

    <div class="zc">
      <a>还没有账号，去注册~</a>
    </div>
  </div>
</template>

<script>
import { login } from '@/api/user'
export default {
  data () {
    return {
      mobile: '',
      code: ''
    }
  },
  methods: {
    onClickLeft () {
      this.$router.back()
    },
    async onSubmit () {
      const res = await login(this.mobile, this.code)
      console.log(res)
    }
  }
}
</script>

<style lang="less" scoped>
.navbar {
  background: #1cb676;
  :deep(.van-nav-bar__title) {
    color: #fff;
  }
  .van-icon {
    color: #fff;
  }
}
.van-field {
  :deep(.van-field__label) {
    flex: 1;
  }
  :deep(.van-field__value) {
    flex: 20;
  }
  :deep(.toutiao) {
    font-size: 0.5rem;
  }
}

.code-btn {
  background-color: #eee;
  padding: 0 10px;
  color: #666;
}
.van-button--info{
  background-color:#1cb676;
}

.zc {
  font-size: 14px;
  text-align: center;
  margin-top: 25px;
  color: #666;
}
</style>
