<template>
  <div class="description-wrapper">

    <vheader message="我的优惠">
      <span class="fa fa-angle-left" @click="goToVip" slot="angle"></span>
    </vheader>

    <div class="markdown">
      <p> 尊敬的用户，随着会员体系逐渐完善，自2016年10月10日起，饿了么会员权益将做如下优化：购卡后31天内，累积享有30单减免配送费服务（每日最多3单，每单最高减免4元）。注：已购买的会员服务不受影响，当前会员服务失效前无法购买新卡。
        </p>
      <h3 id="q1-">Q1: 特权介绍</h3>
      <ul>
        <li>身份标识：饿了么会员服务有效期内，享有专属皇冠标识。</li>
        <li>减免配送费： 饿了么会员卡自绑定账户之日起31天内，在「蜂鸟专送」标识商家下单，享有30次减免配送费特权，每日最多减免3单，每单最高可减4元。</li>
        <li>更多特权，敬请期待！</li>
      </ul>
      <h3 id="q2-">Q2: 资费介绍</h3>
      <ul>
        <li>饿了么会员卡：20元</li>
      </ul>
      <h3 id="q3-">Q3: 使用说明</h3>
      <ul>
        <li>当用户满足以下任一条件，会员服务自动失效：</li>
        <li>自绑定之日起超过31天；</li>
        <li>在31天内累计使用减免配送费的蜂鸟订单数量达到30单；</li>
      </ul>
      <h3 id="q4-">Q4: 购卡说明</h3>
      <ul>
        <li>在线购买：饿了么App&gt;我的&gt;饿了么会员卡</li>
      </ul>
      <h3 id="q5-">Q5: 温馨提示</h3>
      <ul>
        <li>用户在当前会员服务失效前，无法购买新卡。</li>
        <li>请认准饿了么官方渠道，任何从其他第三方途径获得的会员卡，饿了么不保证其可用性。</li>
      </ul>
    </div>
  </div>
</template>
<script>
  import vheader from '../../../../components/header/header.vue'
  export default {
    components: {
      vheader
    },
    data () {
      return {}
    },
    methods: {
      goToVip () {
        this.$root.isShowChildren = false
        window.localStorage.setItem('isShowChildren', false)
        this.$router.push({path: '/vip'})
      }
    }
  }
</script>
<style lang="less" scoped>
  @import '../../../../common/comment.less';
  @import '../../../../common/headerComment.less';
  .description-wrapper {
    .box;
    .pt(1rem);
    background:@default;
    .markdown {
      padding: .2rem;
      background: @default;
      .pb(1rem);
      p{
        padding:0 .8rem;
        font-size:.28rem;
        line-height:.4rem;
      }
      >h3{
        font-size:.32rem;
        .mt(.2rem);
        .mb(.2rem);
      }
      >ul{
        >li{
          font-size:.28rem;
        }
      }
    }
  }

  .vip-slide-enter-active {
    animation: vip-slide-in 0.5s linear;
  }

  @keyframes vip-slide-in {
    0% {
      transform: translateX(100%);
      opacity: 0.3;
    }
    100% {
      transform: translateX(0);
      opacity: 1;
    }
  }

  .vip-wrapper-slide-enter-active {
    animation: vip-wrapper-slide-in 1s linear;
  }

  @keyframes vip-wrapper-slide-in {
    0% {
      opacity: 0;
    }
    100% {
      opacity: 1;
    }
  }
</style>
