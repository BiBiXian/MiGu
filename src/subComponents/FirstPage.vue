<template>
  <div class="indexWrapper">
    <search></search>
    <navigation-bar :dataCode="firstCode"></navigation-bar>
    <div class="wrapper" ref="wrapper">
      <div class="content">
        <banner :dataCode="firstCode.banner"></banner>
        <icon :dataCode="firstCode"></icon>
        <div class="line"></div>
        <div class="pricing">
          <div class="icon">
            <span class="fingerText">戳</span>
            <span class="finger icon-point-right"></span>
          </div>
          <div class="textBox">
            <transition-group name="moveText">
              <i class="text" v-show="currentIndex === index"
                 v-for="(text, index) in firstCode.pricing" :key="index">{{text}}</i>
            </transition-group>
          </div>
        </div>
        <video-list :dataCode="firstCode.film"></video-list>
        <div class="footer">终于让你发现了我的底线</div>
      </div>
    </div>
  </div>

</template>

<script>
  import BScroll from 'better-scroll'
  import {Search, NavigationBar, Banner, Icon, VideoList} from '../widget/index'
  export default {
    created() {
      this.axios('/api/firstCode')
        .then(res => {
          res = res.data
          if (res.errno === 0) {
            this.firstCode = res.data
//              console.log(this.firstCode,123)
            this.$nextTick(() => {
              setInterval(() => {
                this.currentIndex++
                if (this.currentIndex >= this.firstCode.pricing.length) {
                  this.currentIndex = 0
                }
              }, 2000)

              this.wrapperScroll = new BScroll(this.$refs.wrapper, {
                click: true
              })
            })
          }
        })
    },
    data() {
      return {
        firstCode: {},
        currentIndex: 0
      }
    },
    components: {
      Search,
      NavigationBar,
      Banner,
      Icon,
      VideoList
    }
  }
</script>

<style lang="sass" rel="stylesheet/scss" scoped>
  .wrapper
    position: fixed
    top: 66px
    left: 0
    bottom: 53px
    box-sizing: border-box
    width: 100%
    overflow: hidden
    .line
      margin: 12px 8px 16px 15px
      border-top: 1px solid #F5F5F5
    .pricing
      margin: 0 20px
      font-size: 0
      .icon
        display: inline-block
        .fingerText
          margin-right: 4px
          font-size: 18px
          font-weight: bold
          color: #D60419
        .finger
          margin-right: 20px
          font-size: 14px
          color: #D60419
          line-height: 14px
      .textBox
        display: inline-block
        position: relative
        padding-top: 2px
        width: 200px
        height: 18px
        line-height: 18px
        box-sizing: border-box
        overflow: hidden
        .text
          position: absolute
          font-size: 14px
          &.moveText-enter-active
            transition: all 0.5s
          &.moveText-enter
            transform: translateY(100%)
          &.moveText-leave-active
            transition: all 0.5s
          &.moveText-leave-to
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
