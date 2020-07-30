<template>
  <div>
    <Navbar title="个人中心"></Navbar>

    <div>
      <div v-if='userinfo.avatarUrl'>
        <img :src="userinfo.avatarUrl" alt="">
        <div v-text='userinfo.nickName'></div>
      </div>
      <div v-else>
        <button
          open-type='getUserInfo'
          @getuserinfo='getLogin'
          >立即登录</button>
      </div>
    </div>

    <canvas type="2d" id="myCanvas"></canvas>

  </div>
</template>

<script>
import { formatTime } from '@/utils/index'
import card from '@/components/card'
// import { Navbar } from '@/components'
import Navbar from '@/components/navbar/navbar.vue'

export default {
  components: {
    card,
    Navbar
  },

  data () {
    return {
      userinfo: {}
    }
  },
  onShow() {
    // 调接口，获取个人信息
    // 用token换取个人信息  userinfo
    this.getAllUserInfo()

    // canvas
    const query = mpvue.createSelectorQuery()
    query.select('#myCanvas')
      .fields({ node: true, size: true })
      .exec((res) => {
        // 首先 $ 获取dom节点
        const canvas = res[0].node
        // 上下文
        const ctx = canvas.getContext('2d')
        // 画布的尺寸初始化
        const dpr = mpvue.getSystemInfoSync().pixelRatio
        canvas.width = res[0].width * dpr
        canvas.height = res[0].height * dpr
        ctx.scale(dpr, dpr)

        ctx.fillStyle = '#ff0000'
        ctx.fillRect(0, 0, 100, 100)
        // ctx.draw()
        ctx.draw(false, function() {
          mpvue.canvasToTempFilePath({
            destWidth: 100,
            destHeight: 100,
            canvasId: 'myCanvas',
            success(res) {
              console.log('临时路径', res)
            }
          })
        })
      })

  },
  methods: {
    getAllUserInfo() {
      // mpvue.request()
    },
    getLogin(e) {
      // 调接口：把这些东西，发送给自己的后端
      console.log(e.mp.detail.userInfo)
      // 再调一次获取“用户信息”的接口
      this.getAllUserInfo()
      this.userinfo = e.mp.detail.userInfo
    }
  }
}
</script>

<style>
.log-list {
  display: flex;
  flex-direction: column;
  padding: 40rpx;
}

.log-item {
  margin: 10rpx;
}
</style>
