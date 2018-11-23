<template>
  <div class="bg">
    <router-view/>
    <div class="tab">
      <div class="tab-item">
        <router-link to="/first">
          <span class="index"></span>
          <span class="text">首页</span>
        </router-link>
      </div>
      <div class="tab-item">
        <router-link to="/sports">
          <span class="sports"></span>
          <span class="text">体育</span>
        </router-link>
      </div>
      <div class="tab-item">
        <router-link to="/vip">
          <span class="vip"></span>
          <span class="text">VIP</span>
        </router-link>
      </div>
      <div class="tab-item">
        <router-link to="/live">
          <span class="live"></span>
          <span class="text">直播</span>
        </router-link>
      </div>
      <div class="tab-item">
        <router-link to="/mine">
          <span class="mine"></span>
          <span class="text">我的</span>
        </router-link>
      </div>
    </div>
  </div>

</template>

<script>
  export default {
  }
</script>

<style lang="sass" rel="stylesheet/scss" scoped>
  .bg
    background: #fff
    .tab
      position: fixed
      left: 0
      bottom: 0
      display: flex
      padding-top: 5px
      width: 100%
      height: 48px
      background: #fff
      .tab-item
        flex: 1
        text-align: center
        & > a
          display: block
          font-size: 8px
          color: rgb(77, 85, 93)
          & > span
            display: block
            margin: 0 auto 4px
            width: 28px
            height: 28px
            &.index
              background: url("../public/img/indexIcon@2.0.jpg")
              background-size: 28px 28px
            &.sports
              background: url("../public/img/sportsIcon@2.0.jpg")
              background-size: 28px 28px
            &.vip
              background: url("../public/img/vipIcon@2.0.jpg")
              background-size: 28px 28px
            &.live
              background: url("../public/img/liveIcon@2.0.jpg")
              background-size: 28px 28px
            &.mine
              background: url("../public/img/mineIcon@2.0.jpg")
              background-size: 28px 28px
          &.active
            color: #D60419
            .index
              background: url("../public/img/indexIcon@1.0.jpg")
              background-size: 28px 28px
            .sports
              background: url("../public/img/sportsIcon@1.0.jpg")
              background-size: 28px 28px
            .vip
              background: url("../public/img/vipIcon@1.0.jpg")
              background-size: 28px 28px
            .live
              background: url("../public/img/liveIcon@1.0.jpg")
              background-size: 28px 28px
            .mine
              background: url("../public/img/mineIcon@1.0.jpg")
              background-size: 28px 28px
</style>
