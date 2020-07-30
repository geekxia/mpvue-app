<template>
<div>
  <div>店铺详情</div>

  <div>广东省深圳市宝安区。。。。。30号</div>
  <button @tap='go'>导航去这里</button>
</div>
</template>

<script>
export default {
  methods: {
    go() {
      // 首先验证用户是否授权了地理定位
      wx.getLocation({
       type: 'gcj02',
       success (res) {
         const latitude = res.latitude
         const longitude = res.longitude
         // 打开微信内置地图
         wx.openLocation({
           address:"这是我的地盘，欢迎来做客",
           name: '这是我的地盘，欢迎来做客',
           latitude,
           longitude,
           scale: 18
         })
       }
      })
    }
  }
}
</script>

<style scoped>
</style>
