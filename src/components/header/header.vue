<template>
  <div class="header">
    <div class="content-wrapper">
      <div class="avatar">
        <img width="64" height="64" :src="seller.avatar">
      </div>
      <div class="content">
        <div class="title">
          <div class="brand"></div>
          <div class="name">{{ seller.name }}</div>
        </div>
        <div class="description">{{ seller.description + "/" + seller.deliveryTime + "分钟送达" }}</div>
        <div v-if="seller.supports" class="supports">
          <div class="icon"></div>
          <div class="support">
            {{ seller.supports[0].description }}
          </div>
        </div>
      </div>
    </div>
    <div class="bulletin-wrapper"></div>
  </div>
</template>

<script type="text/ecmascript-6">
  export default {
    props: {
      seller: {
        type: Object
      }
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
.header
  color: #fff
  background: #000
  .content-wrapper
    padding: 24px 12px 18px 24px
    font-size: 0
    .avatar
      display: inline-block
    .content
      display: inline-block
      padding: 2px 0 2px 16px
      .title
        .name
          font-size: 16px
          font-weight: bold
          line-height: 18px
</style>
