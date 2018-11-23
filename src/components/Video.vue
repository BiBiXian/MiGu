<template>
<div class="videoWrapper">
  <div class="videoPlay">
    <video :src="data.videoUrl" class="player" autoplay controls></video>
    <span class="icon-arrow_lift" @click="back"></span>
  </div>
  <div class="otherContent" ref="other">
    <div class="other">
      <div class="advMoney">天将福利，钻石会员首月仅6元，速抢></div>
      <div class="relevant">
        <div class="title">{{data.name}}</div>
        <div class="icon-circle-down"></div>
        <p class="information">
          <span v-if="data.score" class="score">{{data.score}}分</span>
          <span v-if="data.videoType" class="videoType">剧情 {{data.videoType}}</span>
          <span class="playTimes">{{data.playTimes}}万次播放</span>
        </p>
        <div class="detail">{{data.detail}}</div>
      </div>
      <div class="adv">
        <img src="../public/img/video-adv.png" width="100%" height="102">
      </div>
      <div class="actors" v-if="data.actors">
        <div class="head">
          <span class="star">相关影星</span>
          <span class="member">会员24点抢先看</span>
        </div>
        <div class="person">
          <ul>
            <li v-for="(item, index) in data.actors" :key="index" class="actorsList">
              <div class="photo">
                <img :src="item.photo" width="50" height="50">
              </div>
              <span class="name">{{item.name}}</span>
            </li>
          </ul>
        </div>
      </div>
      <div class="line"></div>
      <div class="elseContent">
        <div class="tip">相关推荐({{data.recommend.length}})</div>
        <div class="play" v-for="(item, index) in data.recommend" :key="index">
          <div class="playPic">
            <img :src="item.playImg" width="100%" height="100%">
            <span class="playScore">{{item.score}}</span>
          </div>
          <span class="playName">{{item.playName}}</span>
        </div>
      </div>
      <div class="elseContent">
        <div class="tip">热门评论</div>
        <div class="ratings">
          <div class="ratingItem" v-for="(rating, index) in data.ratings" :key="index">
            <div class="avatar">
              <img :src="rating.avatar" width="40" height="40">
            </div>
            <div class="rateContent">
              <div class="top">
                <div class="user">
                  <span class="username">{{rating.username}}</span>
                  <span class="time">{{rating.rateTime | time}}</span>
                </div>
                <div class="otherRate">
                  <span class="icon icon-twitch"></span>{{rating.comment.length}}
                  <span class="icon icon-thumb_up"></span>{{rating.good}}
                </div>
              </div>
              <div class="text">{{rating.text}}</div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="rating">
      <input class="ratingText" type="text" value="我来说两句...">
      <div class="msg">
        <span class="icon-favorite"></span>
        <span class="icon-download"></span>
        <span class="icon-share2"></span>
      </div>
    </div>
  </div>
</div>
</template>

<script>
  import BScroll from 'better-scroll'
  import {filterCustomDate} from '../public/js/tool'
  export default {
    created() {
      this.$nextTick(() => {
        this.otherScroll = new BScroll(this.$refs.other, {
          click: true
        })
      })
    },
    data() {
      return {
        data: this.$route.params.data
      }
    },
    methods: {
      back() {
        this.$router.go(-1)
      }
    },
    filters: {
      time(date) {
        return filterCustomDate(date)
      }
    }
  }
</script>

<style lang="sass" rel="stylesheet/scss" scoped>
  .videoWrapper
    width: 100%
    .videoPlay
      position: relative
      width: 100%
      height: 210px
      background: #000000
      .player
        width: 100%
        height: 100%
      .icon-arrow_lift
        position: absolute
        top: 12px
        left: 15px
        font-size: 20px
        color: #ccc
    .otherContent
      position: fixed
      top: 210px
      bottom: 45px
      width: 100%
      overflow: hidden
      .other
        padding: 7px 0
        margin-bottom: 45px
        .advMoney
          padding: 7px 7px
          width: 100%
          font-size: 12px
          border-radius: 3px
          text-align: center
          background: #BC954A
          color: #fff
        .relevant
          margin: 16px 7px 22px
          font-size: 0
          .title
            font-size: 12px
          .icon-circle-down
            padding-right: 15px
            font-size: 10px
            text-align: right
            color: #969696
          .information
            margin-top: 15px
            font-size: 8px
            color: #ABABAB
            .score
              color: #AC9D86
            .videoType
              padding-left: 12px
            .playTimes
              padding-left: 12px
          .detail
            margin-top: 20px
            height: 24px
            font-size: 8px
            overflow: hidden
            color: #ABABAB
        .adv
          height: 102px
          width: 100%
          margin-bottom: 12px
        .actors
          padding: 13px 7px 0px
          .head
            .star
              font-size: 14px
              font-weight: bold
            .member
              padding-left: 12px
              font-size: 8px
              color: #A4A4A4
          .person
            padding: 18px 0
            .actorsList
              display: inline-block
              margin-right: 30px
              text-align: center
              &:last-child
                margin-right: 0
              .photo
                margin-bottom: 5px
                width: 50px
                height: 50px
                border-radius: 50%
                overflow: hidden
              .name
                font-size: 10px
                color: #A4A4A4
        .line
          width: 100%
          height: 7px
          background: #F0F4F3
        .elseContent
          padding: 12px 0
          font-size: 0
          width: 100%
          .tip
            padding-left: 7px
            font-size: 16px
            font-weight: bold
          .play
            display: inline-block
            margin-top: 12px
            padding-right: 5px
            width: 50%
            box-sizing: border-box
            &:nth-child(2n-1)
              padding-left: 5px
              padding-right: 0px
            .playPic
              position: relative
              width: 100%
              height: 184px
              .playScore
                position: absolute
                right: 12px
                bottom: 7px
                font-size: 12px
                color: #cbab26
            .playName
              display: inline-block
              padding: 5px 0 0 10px
              font-size: 12px
          .ratings
            .ratingItem
              display: flex
              padding: 25px 7px 0
              .avatar
                flex: 0 0 40px
                width: 40px
                height: 40px
                border-radius: 50%
                overflow: hidden
              .rateContent
                flex: 1
                font-size: 0
                padding-left: 10px
                .top
                  display: flex
                  height: 40px
                  .user
                    flex: 1
                    font-size: 10px
                    color: #979797
                    .username
                      display: block
                      margin-bottom: 14px
                  .otherRate
                    flex: 1
                    line-height: 40px
                    font-size: 10px
                    text-align: right
                    color: #979797
                    .icon
                      display: inline-block
                      margin: 0 14px
                    .icon-thumb_up
                .text
                  margin-top: 14px
                  font-size: 12px
                  color: #979797

    .rating
      display: flex
      position: fixed
      bottom: 0
      left: 0
      padding: 6px 10px
      width: 100%
      height: 45px
      box-sizing: border-box
      background: #fff
      .ratingText
        display: inline-block
        flex: 0 0 210px
        width: 210px
        border: 1px solid #ccc
        border-radius: 20px
        font-size: 10px
        text-indent: 18px
        color: #C7C8C3
      .msg
        flex: 1
        display: flex
        text-align: center
        &>span
          padding-top: 10px
          flex: 1
          color: #8E8E8E
</style>
