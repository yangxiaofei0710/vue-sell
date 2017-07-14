<template>
  <div id="app">
    <v-header :seller='seller'></v-header>
    <div class="tab border-1px" >
      <div class="tab-item">
        <router-link :to="{ path: 'goods' }" active-class='active'>商品</router-link> 
      </div>
      <div class="tab-item">
        <router-link :to="{ path: 'ratings' }" active-class='active'>评论</router-link>
      </div>
      <div class="tab-item">
        <router-link :to="{ path: 'seller' }" active-class='active'>商家</router-link>
      </div>
    </div>
    <router-view></router-view>
  </div>
</template>

<script>
import  header from '@/components/header/header'

const ERR_OK = 0

export default {
  components: {
    vHeader: header
  },
  data () {
    return {
      seller: {},
    }
  },
  created () {
    this.$http.get('/api/seller').then((res) =>  {
      console.log(res)
      if (res.data.errno === ERR_OK) {
          this.seller = res.body
          console.log(this.seller)
      }
    })
  }
}
</script>

<style lang="less" rel="stylesheet/less">
@import "./common/stylus/mixin.less";

  #app .tab{
    display: flex;
    width: 100%; 
    height: 2.6rem;
    line-height: 2.6rem;
    // border-bottom: 1px solid rgba(7, 17, 27, 0.1);
    .border-1px(rgba(7, 17, 27, 0.1));
    .tab-item {
      flex: 1;
      text-align:center;
      a {
        display:block;
        font-size: 1rem;
        color: rgb(77, 85, 93);
        &.active{
          color: rgb(240, 20, 20);
        }
      }
    }
  }
</style>
