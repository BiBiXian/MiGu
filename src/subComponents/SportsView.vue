<template>
  <div class="sportsWrapper">
    <search></search>
    <navigation-bar :dataCode="sports"></navigation-bar>
    <div class="wrapper" ref="wrapper">
      <div class="content">
        <banner :dataCode="sports.banner"></banner>
        <icon :dataCode="sports"></icon>
        <video-list :dataCode="sports.film"></video-list>
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
      this.axios('/api/sports')
        .then(res => {
          res = res.data
          if (res.errno === 0) {
            this.sports = res.data
          }
        })
    },
    data() {
      return {
        sports: {}
      }
    },
    mounted() {
      this.$nextTick(() => {
        this.wrapperScroll = new BScroll(this.$refs.wrapper, {
          click: true
        })
      })
    },
    components: {
      Search,
      Banner,
      Icon,
      NavigationBar,
      VideoList
    }
  }
</script>

<style lang="sass" rel="stylesheet/scss" scoped>
  .sportsWrapper
    width: 100%
    .wrapper
      position: fixed
      top: 66px
      left: 0
      bottom: 53px
      box-sizing: border-box
      width: 100%
      overflow: hidden
      .footer
        margin-top: 20px
        width: 100%
        height: 30px
        line-height: 30px
        text-align: center
        font-size: 12px
        color: rgb(77, 85, 93)

</style>
