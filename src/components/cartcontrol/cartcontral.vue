<template>
  <div class="cartcontrol">
    <transition name="fade">
      <div class="cart-decrease" v-show="food.count>0" @click="decreaseCart">
        <i class="inner iconfont icon-subtract"></i>
      </div>
    </transition>
    <div class="cart-count" v-show="food.count>0">{{food.count}}</div>
    <div class="cart-add" @click="addCart">
      <i class="iconfont icon-add"></i>
    </div>
  </div>
</template>

<script>
  import  Vue from "vue";
  export default {
      props: {
          food: {
              type: Object
          }
      },
      created() {
      },
      methods: {
          addCart(event) {
            if(!event._constructed){
                return;
            }
            if(!this.food.count){
                Vue.set(this.food, "count", 1);
              } else {
                  this.food.count++;
            }
            this.$emit('cartAdd', event.target);
          },
          decreaseCart(event) {
            if(!event._constructed){
              return;
            }
            if(this.food.count){
                this.food.count--;
            }
          }
      }
  }
</script>

<style lang="less" rel="stylesheet/less/less" scoped>
  .cartcontrol {
    .fade-enter, .fade-leave-to{
      opacity: 0;
      transform: translate3D(24px,0,0) rotate(180deg);
    }
    .fade-enter-to, .fade-leave{
      opacity: 1;
      transform: translate3D(0,0,0);
    }
    .fade-enter-active,.fade-leave-active{
      transition: all 0.3s linear;
    }
    .cart-decrease{
      display: inline-block;
      line-height: 16px;
      padding: 6px;
      font-size: 24px;
    }
    .cart-decrease i, .cart-add i {
      display: inline-block;
      border-radius: 16px;
      padding: 1px;
      background: rgb(0, 160, 220);
      color: #ffffff;
    }
    .cart-count{
      display: inline-block;
      vertical-align: top;
      width: 12px;
      padding-top: 6px;
      line-height: 24px;
      text-align: center;
      font-size: 12px;
      color: rgb(147, 153, 159);
    }
    .cart-add{
      display: inline-block;
      line-height: 16px;
      padding: 6px;
      font-size: 24px;
    }
  }
</style>
