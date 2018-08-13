<template>
  <div class="container">
    <div class="title"><img src="/static/images/lrh_a/logo.png" /></div>
    <div class="titleText">小猪微助手</div>
    <div class="inputDiv">
      <div class="inputLeftImg">
        <img src="/static/images/lrh_a/people_blue.png">
      </div>
      <div class="inputArea">
        <input type="text" class="formControl" v-model="username" placeholder="输入用户名" />
      </div>
    </div>
    <div class="inputDiv">
      <div class="inputLeftImg">
        <img src="/static/images/lrh_a/lock_blue.png">
      </div>
      <div class="inputArea">
        <input type="password" class="formControl" v-model="password" placeholder="输入密码" />
      </div>
    </div>
    <div class="inputDiv">
      <div class="inputLeftImg">
        <img src="/static/images/lrh_a/computer_blue.png">
      </div>
      <div class="inputArea">
        <input type="text" class="formControl" v-model="server" placeholder="输入服务器域名" />
      </div>
    </div>
    <div class="empty"></div>
    <span @click="login" class="bigBtn">登  陆</span>
    <br>
    <div class="modifyLink">
      <!-- <a href='/pages/monitors/serverEdit'>修改服务器地址</a> -->
    </div>
  </div>
</template>
<script>
import { getStorage, setStorage } from '@/utils/wechat'
import { userLogin } from '@/utils/api'
import request from '@/utils/request'
const LAST_SPLASH_DATA = 'LAST_SPLASH_DATA'
const LAST_SUCCESS_LOGIN_INPUT = 'LAST_SUCCESS_LOGIN_INPUT'
const LAST_SUCCESS_LOGIN_TICKET = 'LAST_SUCCESS_LOGIN_TICKET'



export default {
  data() {
    return {
      username: '',
      password: '',
      server: wx.getStorageSync('SERVER_HOST').replace('https://', ''),
    }
  },

  methods: {
    async getCache() {
      try {
        let res = await getStorage(LAST_SPLASH_DATA)
        const { movies, expires } = res.data
        // 有缓存，判断是否过期
        if (movies && expires > Date.now()) {
          return res.data
        }
        // 已经过期
        console.log('uncached')
        return null
      } catch (error) {
        return null
      }
    },

    handleStart() {
      // TODO: 访问历史的问题
      wx.switchTab({
        url: '../board/main'
      })
    },

    async getInitData() {
      let ticketCache = await getStorage(LAST_SUCCESS_LOGIN_TICKET)
      console.log('getInitData', ticketCache)

    },
    async login() {
      // let data = await userLogin({ userName: this.username, password:this.password, count: 3 })
      console.log('https://' + this.server != wx.getStorageSync('SERVER_HOST'))
      if ('https://' + this.server != wx.getStorageSync('SERVER_HOST')) {
        wx.setStorageSync('SERVER_HOST', 'https://' + this.server)
        console.log('cp')
        request.initConfig()
        console.log('cp')
      }
      console.log("wx.getStorageSync('SERVER_HOST')", wx.getStorageSync('SERVER_HOST'))
      let data = await userLogin({ userName: this.username, password: this.password })
      // let data = await userLogin()
      if (data.Result.ReturnFlag._text == '0' && data.Result.ReturnMsg._text == "success") {
        wx.setStorageSync('RECENT_GATEWAYS', 0)
        wx.reLaunch({
          url: '/pages/index'
        })
      }
    }
  },

  mounted() {
    let cache = wx.getStorageSync(LAST_SUCCESS_LOGIN_INPUT)
    if (cache) {
      this.username = cache.userName
      this.password = cache.password
    } else {
      this.username = ''
      this.password = ''
    }
  }
}

</script>
<style scoped>
.container {
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  padding: 20rpx 0;
  box-sizing: border-box;
  background-color: #fff;
}

.inputDiv {
  display: block;
  width: 80%;
  padding: 5px 12px;
  padding-left: 0;
  padding-bottom: 10px;
  margin-bottom: 5px;
  border-bottom: 1px solid #ccc;
  border-radius: 5rpx;
}

.inputArea {
  float: left;
}


.inputLeftImg {
  padding-top: 6px;
  padding-left: 4px;
  float: left;
}

.inputLeftImg img {
  width: 22px;
  height: 22px;
}

.form-container {
  width: 80%;
}

.empty {
  height: 24px;
  width: 100%;
}

.title {
  width: 100%;
  white-space: nowrap;
  text-align: center;
}

.titleText {
  padding-bottom: 24px;
  width: 100%;
  white-space: nowrap;
  text-align: center;
  color: rgb(51, 51, 51);
  font-size: 36px;
  font-style: normal;
  text-decoration: none;
  font-family: 楷体;
}

.title img {
  width: 150px;
  height: 150px;
}

.modifyLink {
  width: 80%;
  padding-top: 40rpx;
  text-align: right;
  font-size: 14px;
}

</style>
