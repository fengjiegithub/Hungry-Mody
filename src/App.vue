<template>
  <div id="app">
    <v-header :seller="seller"></v-header>

    <div class="tab border-1px">
      <div class="tab-item">
        <router-link to="/goods">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/ratings">评论</router-link>
        </div>
      <div class="tab-item">
        <router-link to="seller">商家</router-link></div>
    </div>
     <router-view :seller="seller"></router-view>
  </div>
</template>

<script>
  import header from './components/header/header.vue';
  const ERR_OK = 0;
  export default{
      data() {
          return {
              seller:{}
          }
      },
    created() {
          this.$http.get('/api/seller').then((response) => {
            response = response.body;
            if(response.errno ===ERR_OK){
              this.seller= response.data
//              console.log(this.seller)
            }
          })
    },
      components:{
        "v-header":header
      }
  }
</script>

<style rel="stylesheet/scss" lang="scss">
  @import "./common/sass/mixin.scss";
.tab{
  display: flex;
  width: 100%;
  height: 40px;
  line-height: 40px;
  @include  border-1px(rgba(7,17,27,.1)) ;
}
.tab-item{
    flex: 1;
    text-align: center;
}
.tab-item a{
  display: block;
  color: rgb(77,85,93);
  font-size: 14px;
}
  a.active{
    color: rgb(240,20,20);
  }
</style>
