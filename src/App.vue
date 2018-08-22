<script>
export default {
  created() {
    // 调用API从本地缓存中获取数据
    const logs = wx.getStorageSync('logs') || []
    logs.unshift(Date.now())
    wx.setStorageSync('logs', logs)

    console.log('app created and cache logs by setStorageSync')
  },
  destroyed() {
    console.log('destroyed')
    wx.setStorageSync(LAST_SUCCESS_LOGIN_TICKET, {
      data: { ticket: "" }
    })
  }
}

</script>
<style>
@import './iconfont/iconfont.css';
.container {
  /*
  height: 100vh;
  */
  display: flex;
  align-items: center;
  /*
  background-color: #f8f9fb;
  justify-content: space-between;
*/
  padding: 10rpx 0;
  box-sizing: border-box;
  flex-wrap: wrap;
}

body {
  background-color: #f2f4f5;
}

.bigBtn {
  width: 75%;
  display: inline-block;
  margin: 10px auto;
  padding: 15px 15px;
  text-align: center;
  font-size: 16px;
  color: #fff;
  background-color: #6ac33c;
  border: 1px solid #6ac33c;
  border-radius: 15rpx;
}

.smallBtn {
  display: inline-block;
  margin: 10px auto;
  padding: 5px 10px;
  color: black;
  border: 1px solid #000;
  border-radius: 12rpx;
  box-shadow: 2px 2px 5px #000;
}

.formControl {
  display: block;
  width: 100%;
  padding: 5px 12px;
  padding-left: 40px;
  text-align: center;
  font-size: 14px;
  font-weight: 400;
  font-style: normal;
  font-family: 微软雅黑;
  color: rgb(174, 174, 174);
}


.roomWarn {
  background: red;
  animation: myblink 3s;
  animation-iteration-count: infinite;
}

@keyframes myblink {
  0% {
    background: red;
  }
  50% {
    background: yellow;
  }
  100% {
    background: red;
  }
}

.indexWarn {
  background: white;
  animation: roomBlink 3s;
  animation-iteration-count: infinite;
}

@keyframes roomBlink {
  0% {
    opacity: 0;
  }
  50% {
    opacity: 1;
  }
  100% {
    opacity: 0;
  }
}

.border_bottom {
  clear: both;
  background-color: #dfdfe0;
  height: 1px;
  width: 95%;
  bottom: 0;
}

.column_img img {
  width: 18px;
  height: 18px;
}

.column_box {
  width: 100%;
  height: 48px;
  font-size: 14px;
  line-height: 48px;
  background-color: #fff;
  padding-left: 4%;
  padding-right: 4%;
  position: relative;
  display: flex;
  align-items: center;
  border-radius: 10px;
}

.column_img {
  float: left;
  margin-top: 10px;
  margin-right: 15px;
}

.columnTitle {
  float: left;
  width: 75%;
}


.columnRightDetailNormal {
  padding-right: 30px;
  white-space: nowrap;
  text-align: left;
  font-size: 16px;
  font-weight: 700;
  font-style: normal;
  text-decoration: none;
  font-family: 微软雅黑;
  color: #666666;
}

</style>
