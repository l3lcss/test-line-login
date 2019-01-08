<template>
  <div class="hello">
    <!-- <img src="../assets/btn_login_base.png" alt=""> -->
    <div class="btn-login-line" @click="login()"></div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  methods: {
    async login () {
      window.location.href = 'https://access.line.me/dialog/oauth/weblogin?response_type=code&client_id=1635880494&redirect_uri=https://line-login.netlify.com/&state=123abc'
    }
  },
  mounted () {
    let lineCode = this.$route.query.code
    console.log(lineCode, 'lineCode')
  }
}
</script>

<style>
.btn-login-line {
  background-image: url('../assets/btn_login_base.png');
  width: 303px;
  height: 88px;
  cursor: pointer;
  transition: all 0.3s;
}
.btn-login-line:hover {
  background-image: url('../assets/btn_login_hover.png');
  width: 303px;
  height: 88px;
  cursor: pointer;
}
.btn-login-line:active {
  background-image: url('../assets/btn_login_press.png');
  width: 303px;
  height: 88px;
  cursor: pointer;
}
</style>
