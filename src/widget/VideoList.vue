<template>
  <div class="filmWrapper">
    <ul>
      <li class="film" v-for="(item, index) in dataCode" :key="index">
        <div class="title">
          <h2 class="left">{{item.title}}</h2>
          <div class="right" v-if="item.more">
            <span class="more">{{item.more}}</span>
            <span class="icon-keyboard_arrow_right"></span>
          </div>
        </div>
        <div class="content">
          <div class="video" v-for="msg in item.msg" :key="msg.id" v-if="msg.id < 4"  @click="showVideo(msg)">
            <div class="pic">
              <img :src="msg.pic" width="100%" height="100">
              <span v-if="msg.tip" class="tip">{{msg.tip}}</span>
              <span class="text" v-if="!msg.duration">{{msg.updateEP ? msg.updateEP : msg.score}}</span>
              <span class="text" v-if="msg.duration">{{msg.duration}}</span>
            </div>
            <h4 class="name">{{msg.name}}</h4>
            <p class="description" v-if="msg.description">{{msg.description}}</p>
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    props: {
      dataCode: {
        type: Array,
        require: true
      }
    },
    methods: {
      showVideo(item) {
//        console.log(item)
        this.$router.push({name: 'Video', params: {data: item}})
      }
    }
  }
</script>

<style lang="sass" rel="stylesheet/scss" scoped>
  .filmWrapper
    width: 100%
    .film
      margin-top: 20px
      .title
        display: flex
        padding: 0 10px
        font-size: 0
        .left
          display: inline-block
          flex: 1
          font-size: 14px
          font-weight: bold
        .right
          display: inline-block
          flex: 1
          font-size: 10px
          text-align: right
          line-height: 16px
          .icon-keyboard_arrow_right
            vertical-align: middle
      .content
        .video
          display: inline-block
          margin-top: 14px
          width: 50%
          padding-right: 2px
          box-sizing: border-box
          &:nth-child(2n)
            padding-left: 2px
            padding-right: 0px
          .pic
            position: relative
            width: 100%
            height: 100px
            .tip
              position: absolute
              top: 5px
              right: 5px
              padding: 3px 5px
              font-size: 7px
              border-radius: 10px 0 10px 10px
              background: #E8BB20
              color: #fff
            .text
              position: absolute
              bottom: 8px
              right: 8px
              font-size: 12px
              color: #fff
          .name
            padding: 6px 0 9px 12px
            font-size: 14px
            white-space: nowrap
            overflow: hidden
            text-overflow: ellipsis
          .description
            padding-left: 12px
            font-size: 10px
            color: #ABABAB
            white-space: nowrap
            overflow: hidden
            text-overflow: ellipsis
</style>
