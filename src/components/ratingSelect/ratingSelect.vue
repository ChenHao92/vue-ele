<!--
  @Author: chenhao
  @Date:   2017-03-06 13:45:30
  @Last Modified by:   ch
  @Last Modified time: 2017-03-06 13:45:30
-->
<template>
  <div class="rating-select">
    <div class="rating-type">
      <span class="all" :class="{'highlight': selectType===2}" @click="changeSelectType(2, $event)">{{desc.all}} <span class="count">{{ratings.length}}</span></span>
      <span class="positive" :class="{'highlight': selectType===0}" @click="changeSelectType(0, $event)">{{desc.positive}} <span class="count">{{positive.length}}</span></span>
      <span class="negative" :class="{'highlight': selectType===1}" @click="changeSelectType(1, $event)">{{desc.negative}} <span class="count">{{negative.length}}</span></span>
    </div>
    <div class="switch" @click="showOnlyContent($event)" :class="{'highlight': isOnlyContent === true}">
      <i class="icon-check_circle"></i>
      <span>只看有内容的评价</span>
    </div>
    <ul class="ratings">
      <li class="rating" v-for="rating in showRatings" v-show="selectType === 2 || rating.rateType === selectType">
        <div class="rating-info">
          <span class="time">{{rating.rateTime | formatDate}}</span>
          <span class="user-name">{{rating.username}}</span>
          <img class="user-avatar" :src="rating.avatar">
        </div>
        <div class="rating-content">
          <i :class="classType[rating.rateType]"></i>
          <span>{{rating.text}}</span>
        </div>
      </li>
    </ul>
  </div>
</template>

<script type="text/ecmascript-6">
  import {formatDate} from 'common/js/date';

  const ALL = 2;
  const NEGATIVE = 1;
  const POSITIVE = 0;
  export default {
    props: {
      // 用户评价
      ratings: {
        type: Array,
        default () {
          return [];
        }
      },
      // 显示的评价类型
      selectType: {
        type: Number,
        default: ALL
      },
      // 是否只显示有内容的评价
      isOnlyContent: {
        type: Boolean,
        default: true
      },
      // 按钮描述文字
      desc: {
        type: Object,
        default () {
          return {
            all: '全部',
            positive: '满意',
            negative: '不满意'
          };
        }
      }
    },
    data () {
      return {
        classType: ['icon-thumb_up', 'icon-thumb_down']
      };
    },
    methods: {
      changeSelectType (type, event) {
        if (!event._constructed) {
          return;
        }
       this.selectType = type;
       this.$dispatch('ratingTypeChanged');
      },
      showOnlyContent (event) {
        if (!event._constructed) {
          return;
        }
        this.isOnlyContent = !this.isOnlyContent;
        this.$dispatch('ratingTypeChanged');
      }
    },
    computed: {
      positive () {
        let newRatings = this.ratings.filter((rating) => {
          return rating.rateType === POSITIVE;
        });
        return newRatings;
      },
      negative () {
        return this.ratings.filter((rating) => {
          return rating.rateType === NEGATIVE;
        });
      },
      showRatings () {
        if (!this.isOnlyContent) {
          return this.ratings;
        } else {
          return this.ratings.filter((rating) => {
            return rating.text !== '';
          });
        }
      }
    },
    filters: {
      formatDate (time) {
        let date = new Date(time);
        return formatDate(date, 'yyyy-MM-dd hh:mm');
      }
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  .rating-select
    .rating-type
      font-size: 0px
      line-height: 16px
      margin-bottom: 18px
      span
        display: inline-block
        padding: 8px 12px
        font-size: 12px
        margin-right: 8px
        border-radius: 2px
      .all, .positive
        background: rgba(0,160,220,0.2)
        color: rgb(77,85,93)
        &.highlight
          background: rgb(0,160,220)
          color: #fff
      .negative
        background: rgba(77,85,93,0.2)
        color: rgb(77,85,93)
        &.highlight
          background: rgb(77,85,93)
          color: #fff
      .count
        font-size: 8px
        padding: 0
        margin: 0
    .switch
      padding: 12px 0
      color: rgb(147,153,159)
      &.highlight
        color: rgb(0,160,220)
      .icon-check_circle
        vertical-align: middle
        font-size: 24px
        line-height: 24px
      span
        font-size: 12px
        line-height: 24px
    .ratings
      .rating
        width: 100%
        padding: 16px 0
        border-bottom: 1px solid rgba(7,17,27,0.1)
        .rating-info
          position: relative
          height: 12px
          font-size: 10px
          line-height: 12px
          padding-bottom: 6px
          color: rgb(147,153,159)
          .time
            position: absolute
            left: 0
          .user-name
            position: absolute
            right: 18px
          .user-avatar
            position: absolute
            right: 0
            width: 12px
            height: 12px
            border-radius: 50%
        .rating-content
          font-size: 0
          .icon-thumb_up
            font-size: 12px
            line-height: 24px
            margin-right: 4px
            color: rgb(0,160,220)
          .icon-thumb_down
            font-size: 12px
            line-height: 24px
            margin-right: 4px
            color: rgb(147,153,159)
          span
            font-size: 12px
            color: rgb(7,17,27)
            line-height: 16px
</style>
