<template>
<div class="navbar">
  <span @tap='goBack' class="navbar_back" v-show='back'>返回</span>
  <span class="navbar_title" v-text='title'></span>
</div>

</template>

<script>
export default {
  props: {
    title: {
      type: String,
      required: true
    },
    back: {
      type: Boolean,
      required: false,
      default: true
    }
  },
  methods: {
    goBack () {
      mpvue.navigateBack()
    }
  }
}
</script>

<style lang="css" scoped>
.navbar {
  height: 128rpx;
  width: 100%;
  background-color: white;
  overflow: hidden;
  text-align: center;
  color: black;
  line-height: 128rpx;
}
.navbar_back {
  float: left;
}
</style>
