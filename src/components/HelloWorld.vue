<template>
  <div class="hello">
    <!-- <img src="../assets/btn_login_base.png" alt=""> -->
    <div class="btn-login-line" @click="login()"></div>
  </div>
</template>

<script>
import axios from 'axios'
import querystring from 'querystring'
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  methods: {
    async login () {
      window.location.href = 'https://access.line.me/oauth2/v2.1/authorize?response_type=code&client_id=1635880494&redirect_uri=https%3A%2F%2Fline-login.netlify.com&state=12345abcde&scope=openid%20profile&nonce=09876xyz'
    }
  },
  async mounted () {
    const code = this.$route.query.code
    const data = {
      grant_type: 'authorization_code',
      client_id: '1635880494',
      client_secret: 'd105fd17568b15c6f427b1d1974586e5',
      code,
      redirect_uri: 'https://line-login.netlify.com'
    }
    const options = {
      method: 'POST',
      header: {
        'Access-Control-Allow-Origin': 'https://line-login.netlify.com'
      },
      data: querystring.stringify(data),
      url: 'https://api.line.me/oauth2/v2.1/token'
    }
    console.log(options, 'options')

    // querystring.stringify(data)
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
</style>
