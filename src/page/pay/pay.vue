<template>
  <div class="pay-wrapper">

    <vheader message="在线支付">
      <span @click="$router.go(-1)" class="fa fa-angle-left"  slot="angle"></span>
    </vheader>

    <div class="pay_time">
      <p class="warning_info">支付剩余时间</p>
      <h2 class="remaining_time"><span>00</span> : <span class="minutes" id="minutes">00</span> : <span class="seconds" id="seconds">59</span></h2>
      <p class="intro"><span @click="goToOrderDetail">详情</span><span>￥425</span></p>
    </div>
    <h3 class="change_pay_type">选择支付方式</h3>
    <ul class="pay_type_box">
      <li class="pay_type_wrapper">
        <div class="pay_logo"><img :src="zhifubao"></div>
        <span class="pay_ch">支付宝</span>
        <span class="select_pay_type fa fa-check-circle" :class="{select:zfb}" @click="selectZFB"></span>
      </li>
      <li class="pay_type_wrapper">
        <div class="pay_logo"><img :src="weixin"></div>
        <span class="pay_ch">微信</span>
        <span class="select_pay_type fa fa-check-circle" :class="{select:wx}" @click="selectWX"></span>
      </li>
    </ul>
    <p class="pay_btn" @click="pay">确认支付</p>


    <alertBounced v-if="isOverTime" @closeBounced="isOverTime = false" :alertText="alertText">
    </alertBounced>

  </div>
</template>
<script>
  import vheader from '../../components/header/header.vue'
  import alertBounced from '../../components/bounced/bounced.vue'
  export default {
    data () {
      return {
        zhifubao: require('../../../static/img/zhifubao.png'),
        weixin: require('../../../static/img/weixin.png'),
        isOverTime: false, // 显示弹框
        zfb: true, // 支付宝
        wx: false,  // 微信
        noTime: false,
        hasTime: false,
        timer: '',
        alertText: null
      }
    },
    components: {
      vheader,
      alertBounced
    },
    created () { // 页面一加载刷新就更改数字
      setTimeout(() => {
        this.autoAlert()
      }, 1000)
    },
    methods: {
      selectZFB () {  // 选择支付宝
        this.zfb = true
        this.wx = false
      },
      selectWX () {  // 选择微信
        this.zfb = false
        this.wx = true
      },
      pay () {
        this.isOverTime = true  // 显示弹框
        this.alertText = '当前支付环境无法打开，请打开官方APP进行付款'
      },
      autoAlert () {
        let seconds = document.getElementById('seconds')
        this.timer = setInterval(() => {  // 启动定时器
          let s = parseInt(seconds.innerHTML)
          if (s > 0) {
            s--
            s < 10 ? s = '0' + s : s  // 显示为0x的样式
            seconds.innerHTML = s  // 改变内容
          } else {
            this.isOverTime = true  // 显示弹框
            this.alertText = '支付超时' // 显示支付超时
            clearInterval(this.timer) // 清楚定时器
          }
        }, 1000)
      },
      goToOrderDetail () { // 条转到详情页
        this.$router.push({path: '/order'})
      }
    }
  }
</script>
<style lang="less" scoped>
  @import '../../common/comment.less';
  @import '../../common/headerComment.less';
  .pay-wrapper {
    .box;
    font-size: 0;
    min-height: 100vh;
    background: @f7;
    .pay_time {
      font-size: .24rem;
      background: @default;
      .tc;
      .pt(.6rem);
      .pb(.3rem);
      .remaining_time {
        font-size: .6rem;
        line-height: .8rem;
      }
      .intro {
        .pl(.2rem);
        .pr(.2rem);
        .flex;
        span {
          flex: 1;
          text-align: left;
          font-size: .28rem;
        }
        span + span {
          .tr;
          .fw;
          color: @org;
        }
      }
    }
    .change_pay_type {
      font-size: .28rem;
      .pl(.2rem);
      line-height: .6rem;
    }
    > ul {
      .pay_type_wrapper {
        background: @default;
        padding: .2rem;
        font-size: 0;
        .flex;
        .at;
        .pay_logo {
          flex: 2;
          img {
            width: 100%;
          }
        }
        .pay_ch {
          flex: 7;
          font-size: .32rem;
          .pl(.1rem);
        }
        .select_pay_type {
          flex: 1;
          color: @ddd;
          font-size: .6rem;
        }
        .select {
          color: @button;
        }
      }
      .pay_type_wrapper:first-child{
        border-bottom:1px solid @ddd;
      }
    }
    .pay_btn {
      border: none;
      width: 90%;
      margin: 0 auto;
      background: @button;
      line-height: .6rem;
      .b-r(5px);
      color: @default;
      font-size: .36rem;
      .tc;
      .mt(.3rem);
    }
  }
</style>
