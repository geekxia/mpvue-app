<template>
  <div class="index" @click="clickHandle">
    <img class="img1" :src="img.a" />
  </div>
</template>

<script>
import card from '@/components/card'
import img from "@/utils/img"

export default {
  data () {
    return {
      
      img,
      motto: 'Hello miniprograme',
      userInfo: {
        nickName: 'mpvue',
        avatarUrl: 'http://mpvue.com/assets/logo.png'
      }
    }
  },

  components: {
    card
  },

  methods: {
    bindViewTap () {
      const url = '../logs/main'
      if (mpvuePlatform === 'wx') {
        mpvue.switchTab({ url })
      } else {
        mpvue.navigateTo({ url })
      }
    },
    clickHandle (ev) {
      console.log('clickHandle:', ev)
      // throw {message: 'custom test'}
    }
  },

  created () {
    // let app = getApp()
  }
}
</script>

<style  scoped>
.img1 {
  width: 100%;
}
</style>
