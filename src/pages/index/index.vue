<template>
  <div class="home">

    <!-- 背景图片 -->
    <img class="home-bg" :src="img.homeBg">
    <!-- 搜索框 -->

    <!-- 筛选按钮组 -->
    <div class="home-filter">
      <div>
        <picker
          @change="cateChange"
          :value="curCate"
          range-key='label'
          :range="cates">
            <span v-text='cates[curCate].label'></span>
            <span>*</span>
        </picker>
      </div>
      <div></div>
      <div></div>
      <div></div>
    </div>

    <!-- 商品列表 -->
    <div
      v-for="item in list"
      @tap='skipToDetail(item)'
      :key='item.id' class="home_good">
      <span v-text='item.name'></span>
      <span>-</span>
      <span v-text='item.price'></span>
    </div>

  </div>
</template>

<script>
import card from '@/components/card'
import img from '@/utils/img'
import { goods } from '@/utils/data'

export default {
  config: {
    enablePullDownRefresh: true,
  },
  data () {
    return {
      img,
      curCate: 0,
      cates: [
        { id: 1, label: '手机数码', value: 'a' },
        { id: 2, label: '母婴产品', value: 'b' },
        { id: 3, label: '女士服装', value: 'c' },
        { id: 4, label: '体育用品', value: 'd' }
      ],
      list: []
    }
  },

  components: {
    card
  },

  onPullDownRefresh () {
    console.log('下拉刷新')
    this.list = goods
    setTimeout(() => {
      mpvue.stopPullDownRefresh()
    }, 1500)
  },

  onReachBottom () {
    // 分页
    this.list = [...this.list, ...goods]
  },

  onShow () {
    // 调接口
    this.list = goods
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
    },
    cateChange (e) {
      console.log(e.target.value)
      this.curCate = e.target.value
    },
    skipToDetail (item) {
      mpvue.navigateTo({
        url: '../detail/main?id=' + item.id + '&name=' + item.name
      })
    }
  },

  created () {
    // let app = getApp()
  }
}
</script>

<style scoped>
.home-bg {
  width: 100%;
  height: 528rpx;
}
.home-filter {
  height: 80rpx;
  line-height: 80rpx;
  display: flex;
}
.home-filter>div {
  flex: 1;
  border: 1rpx solid #ccc;
}
.home_good {
  line-height: 350rpx;
  border-bottom: 1rpx solid orange;
}
</style>
