<template>
  <div class="roomItemRow" @click="toRoomDetail(room)">
    <div class="leftLogoArea" v-bind:class='{warnBg:room.Alarm,offlineBg:room.details && room.details[0] == "设备离线"}'>
      <img src='/static/images/lrh_a/home_white.png'>
    </div>
    <div class='rightArea'>
      <div class='roomName'>{{room._attributes.Name}}</div>
      <div class='dataArea'>
        <div v-for="(detail,i2) in room.details" class="detailCell" :key="i2" v-html='detail'></div>
      </div>
    </div>
  </div>
</template>
<script>
import { redirectToRoomDetail } from '@/utils/api'
export default {
  props: {
    room: Object
  },
  methods: {
    toRoomDetail(gateway) {
      redirectToRoomDetail(gateway._attributes.Id)
    },
    procClassBg(gateway) {
      console.log('gateway', gateway)
      if (gateway.Alarm) {
        return "leftLogoArea warnBg"
      } else {
        if (gateway.details && gateway.details[0] == '设备离线') {
          return "leftLogoArea offlineBg"
        } else {
          return "leftLogoArea"
        }
      }
    }
  }
}

</script>
<style>
.roomItemRow {
  overflow: auto;
  clear: both;
  width: 100%;
  margin: 5px 0;
  background-color: white;
}

.leftLogoArea {
  width: 110rpx;
  float: left;
  height: 96px;
  background-color: #67c23a;
  align-items: center;
  justify-content: center;
  display: flex;
  border-radius: 10px 0px 0px 10px;
}

.warnBg {
  background-color: #f56c6c;
}

.offlineBg {
  background-color: #909298;
}

.leftLogoArea img {
  width: 40px;
  height: 40px;
}

.roomName {
  padding: 5px 0;
  background-color: white;
  font-size: 24px;
  font-weight: 700;
  font-style: normal;
  font-family: 楷体;
  color: rgb(51, 51, 51);
  border-bottom: 1rpx solid #cdcdcd;
}

.rightArea {
  overflow: auto;
  float: left;
  width: 640rpx;
}

.dataArea {
  overflow: auto;
  width: 640rpx;
  background-color: white;
  font-size: 14px;
  font-weight: 400;
  font-style: normal;
  font-family: 微软雅黑;
  color: rgb(51, 51, 51);
}

.detailCell {
  float: left;
  text-align: center;
  padding-top: 10px;
  padding-left: 20px;
}

</style>
