<template>
  <div class="vipWrapper">
    <div class="header">
      <div class="top">
        <div class="t-left">
          <div class="avatar">
            <img :src="vipData.avatar" width="25" height="25">
          </div>
          <span class="login">点击登录</span>
        </div>
        <div class="t-right">
          <div class="member">开通会员</div>
          <img :src="vipData.search" class="search">
          <img :src="vipData.shop" class="shop">
          <span class="theatre">特色剧场</span>
        </div>
      </div>
      <navigation-bar :dataCode="vipData"></navigation-bar>
    </div>
    <div class="wrapper" ref="wrapper">
      <div class="content">
        <banner :dataCode="vipData.banner"></banner>
        <div class="welfareWrapper">
          <span class="welfare">福利</span>
          <div class="welfareBox">
            <transition-group name="moveWelfare">
              <i class="welfareText" v-show="currentIndex === index"
                 v-for="(welfare, index) in vipData.welfare" :key="index">{{welfare}}</i>
            </transition-group>
          </div>
        </div>
        <video-list :dataCode="vipData.film"></video-list>
        <div class="footer">终于让你发现了我的底线</div>
      </div>
    </div>
  </div>
</template>

<script>
  import BScroll from 'better-scroll'
  import {Banner, NavigationBar, VideoList} from '../widget'
    export default {
    created() {
      this.axios('/api/vipData')
        .then(res => {
          res = res.data
          if (res.errno === 0) {
            this.vipData = res.data
          }
        })
    },
    data() {
      return {
        vipData: {},
        currentIndex: 0
      }
    },
    mounted() {
      this.$nextTick(() => {
        setInterval(() => {
          this.currentIndex++
          if (this.currentIndex >= this.vipData.welfare.length) {
            this.currentIndex = 0
          }
        }, 2000)
          this.wrapperScroll = new BScroll(this.$refs.wrapper, {
            click: true
          })
      })
      },
    components: {
      NavigationBar,
      Banner,
      VideoList
    }
  }
</script>

<style lang="sass" rel="stylesheet/scss" scoped>
  .header
    background: #000000
    .top
      display: flex
      padding: 6px 12px 0
      .t-left
        flex: 1
        .avatar
          display: inline-block
          width: 25px
          height: 25px
          border-radius: 50%
          overflow: hidden
        .login
          display: inline-block
          margin: 5px 0 0 12px
          vertical-align: top
          font-size: 8px
          color: #E8D2C7
      .t-right
        flex: 1
        font-size: 0
        .member
          display: inline-block
          padding: 3px 6px
          margin-right: 12px
          border: 1px solid #AB9F57
          border-radius: 10px
          font-size: 8px
          vertical-align: top
          color: #E8D2C7
        img
          margin-right: 12px
          width: 20px
          height: 20px
        .theatre
          display: inline-block
          margin-top: 5px
          vertical-align: top
          font-size: 10px
          color: #E8D2C7
  .wrapper
    position: fixed
    top: 66px
    left: 0
    bottom: 53px
    box-sizing: border-box
    width: 100%
    overflow: hidden
    .welfareWrapper
      display: flex
      margin: 15px 15px
      width: 100%
      height: 18px
      .welfare
        padding: 0px 4px
        flex: 0 0 24px
        width: 24px
        font-size: 10px
        border: 1px solid #B3547C
        color: #B3547C
      .welfareBox
        display: inline-block
        position: relative
        flex: 1
        margin-left: 18px
        overflow: hidden
        .welfareText
          position: absolute
          font-size: 14px
          &.moveWelfare-enter-active
            transition: all 0.5s
          &.moveWelfare-enter
            transform: translateY(100%)
          &.moveWelfare-leave-active
            transition: all 0.5s
          &.moveWelfare-leave-to
            transform: translateY(-100%)
    .footer
      margin-top: 20px
      width: 100%
      height: 30px
      line-height: 30px
      text-align: center
      font-size: 12px
      color: rgb(77, 85, 93)
</style>
