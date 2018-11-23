<template>
  <div class="liveWrapper">
    <search></search>
    <div class="liveItem">
      <div class="l-left" ref="liveName">
        <ul class="itemUl">
          <li class="name" :class="index === nameIndex ? 'active' : ''"
              v-for="(data, index) in liveData" :key="index" @click="setNameIndex(index)">{{data.name}}</li>
        </ul>
      </div>
      <div class="l-right" ref="list">
        <ul v-if="!isLoad">
          <li class="list" v-for="(list, index) in liveData[nameIndex].dataList" :key="index">
            <img class="pic" :src="list.pic">
            <div class="data">
              <div class="title">{{list.title}}</div>
              <div class="nowPlaying">{{list.nowPlaying}}</div>
              <div class="time">{{list.startTime}} - {{list.endTime}}</div>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
  import BScroll from 'better-scroll'
  import {Search} from '../widget/index'
  export default {
    created() {
      this.axios('/api/liveData')
        .then(res => {
          res = res.data
            if (res.errno === 0) {
              this.liveData = res.data
              this.isLoad = false
            }
        })
    },
    data() {
      return {
        liveData: [],
        nameIndex: 0,
        isLoad: true
      }
    },
    watch: {
      liveData() {
       this._initDataList()
      }
    },
    methods: {
      setNameIndex(index) {
        this.nameIndex = index
      },
      _initDataList() {
        this.$nextTick(() => {
            this.nameScroll = new BScroll(this.$refs.liveName, {
              click: true
            })
            this.listScroll = new BScroll(this.$refs.list, {
              click: true
            })
        })
      }
    },
    components: {
      Search
    }
  }
</script>

<style lang="sass" rel="stylesheet/scss" scoped>
  .liveItem
    position: fixed
    top: 43px
    bottom: 53px
    display: flex
    width: 100%
    .l-left
      flex: 0 0 80px
      width: 80px
      overflow: hidden
      background: #fff
      .itemUl
        box-sizing: border-box
        border-right: 1px solid #DEDEDE
        .name
          position: relative
          width: 100%
          height: 55px
          line-height: 55px
          text-align: center
          color: #868686
          &.active
            background: #BB954A
            color: #fff
    .l-right
      flex: 1
      padding-left: 19px
      overflow: hidden
      .list
        padding: 12px 0
        border-bottom: 1px solid #DEDEDE
        font-size: 0
        .pic
          width: 50px
          height: 50px
        .data
          display: inline-block
          margin-left: 12px
          font-size: 12px
          vertical-align: top
          .title
            font-weight: bold
            color: #868686
          .nowPlaying
            margin: 10px 0 6px
            color: #9A9A9A
          .time
            font-size: 8px
            color: #9A9A9A
</style>
