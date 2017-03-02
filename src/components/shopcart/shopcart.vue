<template>
  <div class="shopcart">
    <div class="content">
      <div class="content-left">
        <div class="logo-wrapper">
          <div class="logo" :class="{'highlight': this.totalCount > 0}">
            <i class="icon-shopping_cart" :class="{'highlight': this.totalCount > 0}"></i>
          </div>
          <div class="num" v-show="this.totalCount > 0">{{ totalCount }}</div>
        </div>
        <div class="price" :class="{'highlight': this.totalCount > 0}">¥ {{ totalPrice }}</div>
        <div class="desc">另需配送费 ¥ {{ deliveryPrice }}元</div>
      </div>
      <div class="content-right">
        <div class="pay" :class="{'highlight': this.totalPrice - this.minPrice >= 0}">
           {{ payDesc }}
        </div>
      </div>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  export default {
    props: {
      deliveryPrice: {
        type: Number,
        default: 0
      },
      minPrice: {
        type: Number,
        default: 0
      },
      selectFoods: {
        type: Array,
        default () {
          return [];
        }
      }
    },
    computed: {
      totalPrice () {
        let totalPrice = 0;
        this.selectFoods.forEach((food) => {
          totalPrice += food.price * food.count;
        });
        return totalPrice;
      },
      payDesc () {
        if (this.totalPrice === 0) {
          return `¥ ${this.minPrice}起送`;
        } else if ((this.minPrice - this.totalPrice) > 0) {
          return `还差 ¥ ${(this.minPrice - this.totalPrice)}起送`;
        } else {
          return '去结算';
        }
      },
      totalCount () {
        let count = 0;
        this.selectFoods.forEach((food) => {
          count += food.count;
        });
        return count;
      }
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  .shopcart
    position: fixed
    bottom: 0
    left: 0
    z-index: 50
    height: 58px
    width: 100%
    .content
      position: absolute
      left: 0
      bottom: 0
      display: flex
      height: 48px
      width: 100%
      font-size: 0
      color: rgba(255,255,255,0.4)
      .content-left
        flex: 1
        height: 48px
        background: #141d27
        .logo-wrapper
          display: inline-block
          position: relative
          top: -10px
          width: 56px
          height: 56px
          margin: 0 12px
          padding: 6px
          border-radius: 50%
          box-sizing: border-box
          background: #141d27
          .num
            position: absolute
            top: 0
            right: 0
            width: 24px
            height: 16px
            line-height: 18px
            border-radius: 12px
            font-size: 9px
            font-weight: 700
            text-align: center
            color: rgb(255,255,255)
            background-color: rgb(240,20,20)
            box-shadow: 0px 4px 8px 0px rgba(0,0,0,0.4)
          .logo
            width: 100%
            height: 100%
            border-radius: 50%
            background-color: #2b343c
            text-align: center
            &.highlight
              background-color: rgb(0,160,220)
            .icon-shopping_cart
              font-size: 24px
              line-height: 44px
              &.highlight
                color: rgb(255,255,255)
        .price
          display: inline-block
          vertical-align: top
          margin-top: 12px
          padding-right: 12px
          font-size: 16px
          font-weight: 700
          line-height: 24px
          box-sizing: border-box
          border-right: 1px solid rgba(255,255,255,0.1)
          &.highlight
            color: rgb(255,255,255)
        .desc
          display: inline-block
          vertical-align: top
          font-size: 12px
          line-height: 24px
          padding: 12px
      .content-right
        flex: 0 0 105px
        width: 105px
        .pay
          height: 48px
          line-height: 48px
          background: #2b333b
          text-align: center
          font-size: 16px
          color: rgba(255,255,255,0.4)
          font-weight: 700
          &.highlight
            background-color: #00b43c
            color: rgb(255,255,255)
</style>
