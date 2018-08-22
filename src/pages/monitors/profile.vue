<template>
  <div class="container">
    <div class="indexTitleUser">
      <div class="indexTitleUserLeft"><img src="/static/images/lrh_a/custon_blue.png"></div>
      <div class="indexTitleUserRight"> 当前用户
        <br><span class="currentUser">{{username}}</span></div>
      <div class="version">版本号：1.0</div>
    </div>
    <div class="column_box" @click='goLogin'>
      <div class="column_img"><img src="/static/images/lrh_a/cpeople_green.png"></div>
      <div class="columnTitle">切换用户</div>
      <div class="columnRightDetailNormal"><i class="iconfont icon-jiantouyou"></i></div>
    </div>
    <!-- <div class="border_bottom"></div>
    <div class="column_box" @click='goServerEdit'>
      <div class="column_img"><img src="/static/images/a/server.png"></div>
      <div class="columnTitle">设置服务器</div>
      <div class="columnRightDetailNormal"><img class="arrowImg" src="/static/images/a/arrow_right.png"></div>
    </div> -->
    <div class="border_bottom"></div>
    <div class="column_box" @click='logout'>
      <div class="column_img"><img src="/static/images/lrh_a/people_yellow.png"></div>
      <div class="columnTitle">注销用户</div>
      <div class="columnRightDetailNormal"><i class="iconfont icon-jiantouyou"></i></div>
    </div>
    <!-- <a class="bigBtn" href="login">
      重新登录
    </a>
    <a class="bigBtn" href="serverEdit">
      设置服务器
    </a>
    <span class="bigBtn" @click='logout'>
      注销
    </span> -->
  </div>
</template>
<script>
const LAST_SUCCESS_LOGIN_INPUT = 'LAST_SUCCESS_LOGIN_INPUT'
const LAST_SUCCESS_LOGIN_TICKET = 'LAST_SUCCESS_LOGIN_TICKET'
export default {
  data() {
    return {
      username: '',
    }
  },
  methods: {
    goLogin() {
      wx.navigateTo({ url: '/pages/monitors/login' })
    },
    goServerEdit() {
      wx.navigateTo({ url: '/pages/monitors/serverEdit' })
    },
    logout() {
      wx.showModal({
        title: '是否注销',
        success: function(res) {
          if (res.confirm) {
            wx.setStorageSync(LAST_SUCCESS_LOGIN_INPUT, false)
            wx.setStorageSync(LAST_SUCCESS_LOGIN_TICKET, false)
            wx.redirectTo({ url: '/pages/monitors/login' })
          }
        }
      })
    },
  },
  mounted() {
    let cache = wx.getStorageSync(LAST_SUCCESS_LOGIN_INPUT)
    this.username = cache.userName
  }
}

</script>
<style scoped>
.lineLeft {
  float: left
}

.lineRight {
  float: right
}

.lineArea {
  background-color: #fff;
  padding: 20px 20px 20px 40px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  border-bottom: 1rpx solid #bbb;
}

.profileArea {
  width: 100%;
}

body {
  background-color: #f8f9fb;
  display: flex;
  align-items: center;
  justify-content: center;
}


.container {
  height: 100vh;
  display: block;
  /*
  
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  */
  box-sizing: border-box;
  background-color: #f2f3f5;
}


.arrowImg {
  padding-top: 3px;
  width: 24px;
  height: 24px;
}

.column_box {
  padding-left: 20px;
}

.indexTitleUser {
  left: 0px;
  top: 0px;
  width: 100%;
  color: white;
  padding: 15px 28px;
  display: flex;
  /*
  flex-direction: column;
  */
  align-items: center;
  font-size: 20px;
  font-weight: 400;
  font-style: normal;
  font-family: 微软雅黑;
  color: rgb(0, 0, 0);
  box-sizing: border-box;
  border-radius: 10px;
  background-color: white;
  margin: 20rpx 0;
}

.indexTitleUserLeft {
  float: left
}

.indexTitleUserLeft img {
  width: 56px;
  height: 56px;
}

.currentUser {
  font-size: 16px;
  font-weight: 400;
  font-style: normal;
  font-family: 微软雅黑;
  color: rgb(0, 0, 0);
}

.indexTitleUserRight {
  float: left;
  text-align: right;
  padding-left: 20px;
}

.column_img img {
  width: 32px;
  height: 32px;
}

.column_img {
  padding-top: 4px;
}

.columnTitle {
  float: left;
  width: 75%;
  font-size: 18px;
  font-weight: 400;
  font-style: normal;
  font-family: 微软雅黑;
  color: rgb(0, 0, 0);
}

.version {
  clear: both;
  float: right;
  width: 300rpx;
  height: 20px;
  font-size: 32rpx;
  font-weight: 400;
  font-style: normal;
  font-family: 微软雅黑;
  color: rgb(0, 0, 0);
  text-align: right;
  display: table-cell;
  vertical-align: bottom;
  padding-top: 40px;
}

</style>
