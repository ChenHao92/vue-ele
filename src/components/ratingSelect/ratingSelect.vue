<!--
  @Author: chenhao
  @Date:   2017-03-06 13:45:30
  @Last Modified by:   ch
  @Last Modified time: 2017-03-06 13:45:30
-->
<template>
  <div class="rating-select">
    <div class="rating-type">
      <span class="all">{{desc.all}}</span>
      <span class="positive">{{desc.positive}}</span>
      <span class="negative">{{desc.negative}}</span>
    </div>
    <div class="switch">
      <i class="icon-check_circle"></i>
      <span>只看有内容的评价</span>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  const ALL = 0;
  // const NEGATIVE = 1;
  // const POSITIVE = 2;

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
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  .rating-select
    .rating-type
      font-size: 0px
      line-height: 16px
      span
        display: inline-block
        padding: 8px 12px
        font-size: 12px
        margin-right: 8px
        border-radius: 2px
      .all
        background: rgb(0,160,220)
        color: #fff
      .positive
        background: rgba(0,160,220,0.2)
        color: rgb(77,85,93)
      .negative
        background: rgba(77,85,93,0.2)
        color: rgb(77,85,93)
    .switch
      margin: 12px 0
      .icon-check_circle
        vertical-align: middle
        font-size: 24px
        line-height: 24px
        color: rgb(147,153,159)
      span
        font-size: 12px
        color: rgb(147,153,159)
        line-height: 24px
</style>
