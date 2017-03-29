<template>
  <div class="goods">
    <!--左侧选项列表-->
    <div class="menu-wrap">
      <ul>
        <li v-for="item in goods" class="menu-item">
          <span class="text border-1px">
            <span v-show="item.type>0" class="icon" :class="classMap[item.type]"></span>{{item.name}}
          </span>
        </li>
      </ul>
    </div>
    <!--右侧商品列表-->
    <div class="foods-wrap">
      <ul>
        <li v-for="item in goods" class="food-list">
          <h1 class="title">{{item.name}}</h1>
          <ul>
            <li v-for="food in item.foods" class="food-item">
              <div class="icon">
                <img :src="food.icon" alt="" width="57" height="57">
              </div>
              <div class="content">
                <h2 class="name">{{food.name}}</h2>
                <p class="desc">{{food.description}}</p>
                <div class="extra">
                  <span class="count">月售{{food.sellCount}}份</span>
                  <span>好评率{{food.rating}}%</span>
                </div>
                <div class="price">
                  <span class="now">￥{{food.price}}</span>
                  <span v-show="food.oldPrice" class="old">￥{{food.oldPrice}}</span>
                </div>
              </div>
            </li>
          </ul>
        </li>
      </ul>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  const ERR_OK = 0;
  export default{
    porps: {
      seller: {
        type: Object
      }
    },
    data(){
      return {
        goods: []
      }
    },
    created(){
      this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];
      this.$http.get('/api/goods').then((response) => {
        response = response.body;
        if (response.errno === ERR_OK) {
          this.goods = response.data;
          console.log(this.goods);
        }
      })
    }
  };
</script>
<style rel="stylesheet/scss" lang="scss">
  @import "../../common/sass/mixin.scss";

  .goods {
    position: absolute;
    width: 100%;
    top: 174px;
    display: flex;
    overflow: hidden;
    bottom: 46px;
  }

  .menu-wrap {
    flex: 0 0 80px;
    width: 80px;
    background: #f3f5f7;
    .menu-item {
      display: table;
      height: 54px;
      width: 56px;
      line-height: 14px;
      padding: 0 12px;
      .icon {
        display: inline-block;
        width: 12px;
        height: 12px;
        margin-right: 2px;
        background-size: 12px;
        background-repeat: no-repeat;
        vertical-align: top;
        &.decrease {
          @include bg-image('decrease_3');
        }
        &.descount {
          @include bg-image('discount_3');
        }
        &.guarantee {
          @include bg-image('guarantee_3');
        }
        &.invoice {
          @include bg-image('invoice_3');
        }
        &.special {
          @include bg-image('special_3');

        }
      }
      .text {
        @include border-1px(rgba(7, 17, 27, .1));
        font-size: 12px;
        display: table-cell;
        width: 56px;
        vertical-align: middle;
      }
    }
  }

  .foods-wrap {
    flex: 1;
    .title {
      padding-left: 14px;
      height: 26px;
      line-height: 26px;
      border-left: 2px solid #d9dde1;
      font-size: 12px;
      color: rgb(147, 153, 159);
      background: #f3f5f7;
    }
    .food-item {
      display: flex;
      margin: 18px;
      padding-bottom: 18px;
      @include border-1px(rgba(7, 17, 27, .1));
      &:last-child {
        @include border-none();
        margin-bottom: 0;
      }
      .icon{
        flex: 0 0 57px;
        margin-right: 10px;
      }
      .content{
        flex: 1;
        .name{
          margin: 2px 0 8px;
          height: 14px;
          font-size: 14px;
          color:rgb(7,17,27);
          line-height: 14px;
        }
        .desc,.extra{
          margin-bottom: 8px;
          line-height: 10px;
          font-size: 10px;
          color: rgb(147,153,159);
        }
        .extra{
          margin-bottom:0;
          &.count{
            margin-right: 12px;
          }
        }
        .price{
          font-weight: 700;
          line-height: 24px;
          .now{
            margin-right: 18px;
            font-size: 14px;
            color: rgb(240,20,20);
          }
          .old{
            text-decoration: line-through;
            font-size: 10px;
            color: rgb(147,153,159);
          }
        }
      }
    }
  }
</style>
