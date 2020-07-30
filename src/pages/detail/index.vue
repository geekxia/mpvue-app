<template>
  <div>
    <button @tap='phone'>打电话</button>

    <div>
      <button open-type='share'>
        <text>分享</text>
      </button>
    </div>

    <div class="detail-tab">
      <span @tap='changeTab(0)' :class="{'on':tab===0}">商品</span>
      <span @tap='changeTab(1)' :class="{'on':tab===1}">店铺</span>
      <span @tap='changeTab(2)' :class="{'on':tab===2}">活动</span>
    </div>

    <swiper :current='tab' @change='swiperChange'>
        <block>
          <swiper-item>
            <view class="detail-content">A容器</view>
          </swiper-item>
        </block>
        <block>
          <swiper-item>
            <view class="detail-content">B容器</view>
          </swiper-item>
        </block>
        <block>
          <swiper-item>
            <view class="detail-content">C容器</view>
          </swiper-item>
        </block>
    </swiper>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      tab: 0
    }
  },
  onLoad (options) {
    console.log('动态参数', options)
  },
  onShareAppMessage: function (res) {
    if (res.from === 'button') {
      // 来自页面内转发按钮
      console.log('share', res.target)
    }
    return {
      title: '自定义转发标题',
      path: '/page/user?id=123'
    }
  },
  methods: {
    phone () {
      mpvue.makePhoneCall({
        phoneNumber: '13202264877'
      })
    },
    changeTab(idx) {
      this.tab = idx
    },
    swiperChange(e) {
      this.tab = e.target.current
    }
  }
}
</script>

<style scoped>
.detail-content {
  height: 300rpx;
  border: 1rpx solid #ccc;
  background: orange;
  text-align: center;
  font-size: 100rpx;
  color: white;
}
.detail-tab {
  display: flex;
}
.detail-tab span {
  flex: 1;
  text-align: center;
  line-height: 80rpx;
}
.detail-tab span.on {
  color: red;
}
</style>
