<template>
  <div class="hello">
    <div class="btn-login-line" @click="login()"></div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  methods: {
    async login () {
      window.location.href = 'https://access.line.me/oauth2/v2.1/authorize?response_type=code&client_id=1635880494&redirect_uri=https://line-login.netlify.com&state=login&scope=openid%20profile&nonce=test'
    }
  },
  async mounted () {
    const code = this.$route.query.code
    const options = {
      method: 'POST',
      data: {
        code,
        redirect_uri: 'https://line-login.netlify.com'
      },
      url: 'https://herolcu-test.herokuapp.com/line-token'
    }

    if (code) {
      try {
        let res = await axios(options)
        console.log(res, 'res')
      } catch (error) {
        console.log(error, 'error')
      }
    }
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
.btn {
  text-align: center;
  font-family: 'Courier New', Courier, monospace;
  margin-top: 5rem;
  background-color: cadetblue;
  width: 303px;
  height: 88px;
  cursor: pointer;
  transition: all 0.3s;
}
</style>
