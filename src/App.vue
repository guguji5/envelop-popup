<template>
  <div id="app">
    <div class="content">
      <h3 class="title">信封特效：</h3>
      <ol :class="{show: !showEnvelope}">
        <li>点击"敬启"后高亮，并向上移动10px</li>
        <li>整个信封向下平移100px</li>
        <li>"敬启"消失，滴滴云logo消失</li>
        <li>信封上半部沿Z轴向外旋转180度，同时z-index下降，信封正面慢慢向下</li>
        <li>信封下半部分沿Z轴转动小幅度</li>
        <li>信纸弹出，"随便看看"淡入</li>
      </ol>
      <br />
      <a href="https://github.com/guguji5/envelop-popup">去Github看看</a>
    </div>
     <div class="shadow" v-if="showEnvelope" @click.self="showEnvelope = false">
      <div class="envelop" :class="{'open': openedEnvelope}">
        <div class="top">
          <div class="invitation"></div>
        </div>
        <div class="front"></div>
        <div class="paper">
          <div class="head-left">
            <p class="title">尊敬的 guguji5 ，</p>
            <p class="time">今天是您成为滴滴云用户的 <span class="hot">200</span> 天，感恩！</p>
            <p class="desc">为答谢您一直以来的厚爱，我们诚挚的邀请您加入“<span class="hot">推广返利计划</span>”，期望您在享受滴滴云优质服务的同时，也将他们推广给更多有需要的企业和朋友们。同时，会将推广获得收益返利给长久以来一直支持我们的您。</p>
            <p class="desc">此致，敬礼</p>
          </div>
          <div class="head-content">
            <div class="head-content-item">
              <div class="item-logo item-logo-envoy">
                <img
                  v-if="clueAnimation"
                  class="item-logo-gold"
                  :src="require(`./assets/gold.png`)">
                <span class="title">'最高返利50%'</span>
                <span  v-if="envoyAnimation" class="item-logo-center-shadow"></span>
                <img
                  class="item-logo-center"
                  :class="{'item-logo-center-down-active': envoyAnimation}"
                  :src="require(`./assets/envoy-center.png`)">
                <img
                  class="item-logo-center"
                  :class="{'item-logo-center-up-active': envoyAnimation}"
                  :src="require(`./assets/envoy-center-active.png`)">
                <img class="item-logo-bottom" :src="require(`./assets/envoy-bottom.png`)">
              </div>
              <template>
                <p class="item-desc">
                  成为云使者，推荐用户消费，独享新用户30天内全订单返现，最高享受50%返利。
                  <a href="">了解详情</a>
                </p>
                <button type="primary" class="submit-btn" @click="addAnimation('envoy')">成为云使者</button>
              </template>
            </div>
            <div class="head-content-item">
              <div class="item-logo item-logo-clue">
                <img
                  v-if="clueAnimation"
                  class="item-logo-gold"
                  :src="require(`./assets/gold.png`)">
                <span class="title">{{clueAccount ? '长期返利' : '多重返利'}}</span>
                <span v-if="clueAnimation" class="item-logo-center-shadow"></span>
                <img
                  class="item-logo-center"
                  :class="{'item-logo-center-down-active': clueAnimation}"
                  :src="require(`./assets/clue-center.png`)">
                <img
                  class="item-logo-center"
                  :class="{'item-logo-center-up-active': clueAnimation}"
                  :src="require(`./assets/clue-center-active.png`)">
                <img class="item-logo-bottom" :src="require(`./assets/clue-bottom.png`)">
              </div>
              <template>
                <p class="item-desc">
                  提交您身边有企业上云或云计算服务需求的商机，一旦成单，您可以从该线索的支付订单中获得永久返佣。
                  <a href="">了解详情</a>
                </p>
                <button type="primary" class="submit-btn" @click="addAnimation('clue')">提交企业线索</button>
              </template>
            </div>
            <div class="head-content-item">
              <div class="item-logo item-logo-ai">
                <img
                  v-if="aiAnimation"
                  class="item-logo-gold"
                  :src="require(`./assets/gold.png`)">
                <span class="title">折扣/返利两不误</span>
                <span v-if="aiAnimation" class="item-logo-center-shadow"></span>
                <img
                  class="item-logo-center"
                  :class="{'item-logo-center-down-active': aiAnimation}"
                  :src="require(`./assets/ai-center.png`)">
                <img
                  class="item-logo-center"
                  :class="{'item-logo-center-up-active': aiAnimation}"
                  :src="require(`./assets/ai-center-active.png`)">
                <img class="item-logo-bottom" :src="require(`./assets/ai-bottom.png`)">
              </div>
              <template >
                <p class="item-tip">
                  2020年9月26日加入AI大师
                </p>
                <div class="item-data">
                  <div class="item">
                    <p class="amount"><span>Lv.1 9</span>折</p>
                    <p>当前等级</p>
                  </div>
                  <span class="split"></span>
                  <div class="item">
                    <p class="amount"><span>99</span>元</p>
                    <p>累计返利</p>
                  </div>
                </div>
                <button class="more-btn" @click="addAnimation('ai-master')">查看更多</button>
              </template>
            </div>
          </div>
        </div>
        <div class="bottom">
          <div class="logo"></div>
        </div>
        <div class="goon" @click="showEnvelope = false">随便看看</div>
        <div class="btn" @click="openEnvelop">
          <img :src="require('./assets/seal-word.png')">
        </div>
        <div class="left flower"></div>
        <div class="right flower"></div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data () {
    return {
      openedEnvelope: false,
      showEnvelope: true,
      envoyAnimation: false,
      clueAnimation: false,
      aiAnimation: false,
      clueAccount: {
      },
      envoyAccount: {
      },
      aiAccount: {
      },
    }
  },
  methods: {
    openEnvelop () {
      this.openedEnvelope = true
    },
    addAnimation (type) {
      this[`${type}Animation`] = true
      setTimeout(_ => {
        this[`${type}Animation`] = false
      }, 1500)

      setTimeout(() =>{
        window.open('https://www.didiyun.com', '_blank')
      }, 3000)
    },
  }
}
</script>

<style lang="postcss">
html, body{
  box-sizing: border-box;
  width: 100%;
  height: 100%;
}
#app{
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
.content{
  padding: 40px 30px;
  ol{
    margin-left: 40px;
    opacity: 0;
    &.show{
      opacity: 100;
      transition: opacity 1.5s;
    }
  }
}
*, *::before, *::after {
    box-sizing: inherit;
    padding: 0px;
    margin: 0px;
}
@keyframes Falling {
  0% {
    opacity: 1;
    transform: translateY(-120px);
  }
  100% {
    opacity: 1;
    transform: translateY(240px);
  }
  
}
@keyframes centerDown {
  0% {
    opacity: 1;
    transform: translateY(0px);
  }
  100% {
    transform: translateY(80px);
    opacity: 0;
  }
  
}
@keyframes centerUp {
  0% {
    opacity: 0;
    transform: translateY(80px);
  }
  100% {
    transform: translateY(0px);
    opacity: 1;
  }
  
}
@keyframes Rotate {
  0% {
    opacity: 1;
    transform: rotate(0)
  }
  100% {
    opacity: 1;
    transform: rotate(180deg)
  }
}

.shadow{
  position: fixed;
  left: 0px;
  top: 0px;
  width: 100%;
  height: 100%;
  background:rgba(16, 23, 36, 0.64);
  z-index: 5000;
  .envelop{
    width: 864px;
    height: 406px;
    background: url('././assets/envelop-back.png') no-repeat;
    background-size: 864px 406px;
    position: absolute;
    border-radius: 4px;
    top: 50%;
    left: 50%;
    margin-left: -432px;
    margin-top: -300px;
    z-index: 5001;
    
    .front{
      position: absolute;
      top: 0px;
      left: 0px;
      width: 864px;
      height: 406px;
      background: url('././assets/envelop-front.png') no-repeat;
      background-size: 864px 406px;
      z-index: 5003;
      border-radius: 0px 0px 4px 4px;
    }
    .paper{
      position: absolute;
      top: 15px;
      left: 40px;
      width: 784px;
      height: 390px;
      background: url('././assets/envelop-paper.png') no-repeat;
      background-size: 784px 492px;
      z-index: 5002;
      padding: 30px 40px;
      overflow: hidden;

      .head-left{
        width: 100%;
        margin-bottom: 24px;
        .time{
          margin-bottom: 0px;
        }
        .desc{
          width: 100%;
        }
      }
    }
    .top{
      position: absolute;
      top: 0px;
      left: 0px;
      width: 864px;
      height: 293px;
      background: url('././assets/envelop-top.png') no-repeat;
      background-size: 864px 293px;
      z-index: 5005;
      display: flex;
      padding-top: 92px;
      justify-content: center;

      .invitation{
        width: 94px;
        height: 28px;
        background: url('././assets/invitation.png') no-repeat;
        background-size: 94px 28px;
      }
    }
    .bottom{
      position: absolute;
      bottom: 0px;
      left: 0px;
      width: 864px;
      height: 249px;
      background: url('././assets/envelop-bottom.png') no-repeat;
      background-size: 864px 249px;
      z-index: 5004;
      display: flex;
      padding-top: 190px;
      justify-content: center;
      border-radius: 0px 0px 4px 4px;

      .logo{
        width: 99px;
        height: 33px;
        background: url('././assets/envelop-logo.png') no-repeat;
        background-size: 99px 33px;
      }
      
    }
    .goon{
        position: absolute;
        left: 50%;
        bottom: 70px;
        opacity: 0%;
        transform: translateX(-50%);
        border: 1px solid #fff;
        border-radius: 2px;
        padding: 5px 16px;
        color: #fff;
        font-family: PingFangSC-Medium;
        font-size: 12px;
        line-height: 20px;
        height: 30px;
        z-index: 5007;
      }
    .btn{
      position: absolute;
      top: 200px;
      left: 50%;
      margin-left: -53px;
      width: 107px;
      height: 105px;
      background: url('././assets/seal.png') no-repeat;
      background-size: 107px 105px;
      z-index: 5006;
      img{
        opacity: 0;
        width:107px; 
        height: 105px;
      }
    }
    .flower{
      position: absolute;
      bottom: -13px;
      width: 216px;
      height: 48px;
      background: url('././assets/silk.png') no-repeat;
      background-size: 216px 48px;
      z-index: 5007;
      &.right{
        right: -40px;
      }
      &.left{
        width: 40px;
        left: -40px;
      }
      
    }
    &.open{
      margin-top: -100px;
      transition: margin-top 0.5s ease 0.5s;
      border-radius: 0px 0px 4px 4px;
      .btn{
        top: 170px;
        opacity: 0;
        z-index: 5001;
        transition: top 0.5s, opacity 0.2s ease 1s, z-index 0.2s ease 1s;
        img{
          opacity: 100;
          transition: opacity 0.5s;
        }
      }
      .bottom{
        .logo{
          opacity: 0;
          transition: opacity 0.2s ease 1s;
        }
        
        transform-origin: center bottom; 
        transform: rotateX(50deg);
        transition: transform 0.3s ease 1.5s;
      }
      .goon{
          opacity: 100;
          transition: opacity 0.3s ease 1.7s;
        }
      .top{
        z-index: 5001;
        .invitation{
          opacity: 0;
          transition: opacity 0.2s ease 1s;
        }
        transform-origin: center top; 
        transform: rotateX(180deg);
        transition: transform 0.5s ease 1.3s, z-index 0.1s ease 1.5s;
      }
      .front{
        height: 197px;
        top: 210px;
        transition: all 0.5s ease 1.3s;
      }
      .paper{
        top: -215px;
        height: 492px;
        transition: all 0.5s ease 2s;
      }
    }
  }
}

.head {
    padding: 24px 44px 24px 20px;
    width: 100%;
    height: 302px;
    background: #ECF0F5;
    border-radius: 2px;
    display: flex;
    margin-bottom: 16px;
    &-left {
      width: 380px;
      p {
        font-family: PingFangSC-Regular;
        font-size: 12px;
        color: #303A51;
        text-align: justify;
        line-height: 20px;
        &.title {
          font-family: PingFangSC-Semibold;
          font-size: 14px;
          color: #101724;
          line-height: 22px;
        }
        &.desc {
          width: 260px;
        }
        &.time {
          margin: 16px 0;
          span {
            font-family: DINAlternate-Bold;
            font-size: 16px;
          }
        }
        &.thank {
          margin: 8px 0 32px;
        }
        &.amount {
          font-family: PingFangSC-Semibold;
          font-size: 14px;
          color: #101724;
          line-height: 22px;
          span {
            display: inline-block;
            margin: 8px 0;
            font-family: DINAlternate-Bold;
            font-size: 28px;
          }
        }
        &.title .hot {
          font-size: 20px;
        }
        &.split {
          margin: 0 4px;
          width: 2px;
          height: 14px;
          display: inline0-block;
          background: #E3E6EC;
        }
        .hot {
          color: #ef645c;
        }
      }
      .tip {
        font-family: PingFangSC-Regular;
        font-size: 12px;
        color: #505568;
        line-height: 20px;
      }
      .operate {
        margin-top: 32px;
        display: flex;
        align-items: center;
        .button {
          width: 100px;
          margin-right: 16px;
        }
      }
    }
    &-content {
      flex: 1;
      display: flex;
      justify-content: space-between;
      &-item {
        flex: 1;
        min-width: 208px;
        height: 300px;
        display: flex;
        flex-direction: column;
        align-items: center;
        .item {
          &-logo {
            position: relative;
            width: 160px;
            height: 134px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            border-radius: 80px 80px 0 0;
            overflow: hidden;
            .title {
              display: inline-block;
              position: absolute;
              top: 12px;
              font-family: PingFangSC-Medium;
              font-size: 12px;
              text-align: justify;
            }
            &-gold {
              display: inline-block;
              width: 200px;
              height: 123px;
              top: 0;
              left: -20px;
              position: absolute;
              opacity: 0;
              animation: Falling 1.5s linear .8s 1;
              z-index: 2;
            }
            &-envoy {
              color: #8493AB;
              background-image: linear-gradient(180deg, rgba(191,208,235,0.50) 0%, rgba(191,208,235,0.00) 80%, transparent);
            }
            &-clue {
              color: #B79675;
              background-image: linear-gradient(180deg, rgba(243,227,210,0.50) 0%, rgba(241,221,200,0.00) 80%, transparent);
            }
            &-ai {
              color: #BD9145;
              background-image: linear-gradient(180deg, rgba(255,239,186,0.50) 0%, rgba(237,226,188,0.00) 80%, transparent);
            }
            &-center {
              position: absolute;
              width: 160px;
              height: 134px;
              z-index: 3;
              &-up-active {
                opacity: 0;
                animation: centerUp 1s ease-out 0.5s 1;
                z-index: 5;
              }
              &-down-active {
                opacity: 1;
                z-index: 4;
                animation: centerDown 1s ease 0.5s 1;
              }
              &-shadow {
                width: 80px;
                height: 80px;
                margin-bottom: -20px;
                background-image: linear-gradient(to bottom left, rgba(255,255,255,0.15) 50%, rgba(255,255,255,0.01) 50%); 
                border-radius: 50%;
                z-index: 6;
                opacity: 0;
                animation: Rotate 0.5s ease-in 1;
              }
            }
            &-bottom {
              position: absolute;
              bottom: 0;
              width: 120px;
              height: 19px;
              z-index: 4;
            }
          }
          &-desc {
            width: 208px;
            padding: 15px 0 24px;
            height: 90px;
            font-family: PingFangSC-Regular;
            font-size: 12px;
            color: #303A51;
            text-align: justify;
            .link {
              color: #2F81F9;
              cursor: pointer;
            }
          }
          &-tip {
            height: 32px;
            padding: 15px 0 4px;
            font-family: PingFangSC-Regular;
            font-size: 12px;
            color: #303A51;
            text-align: justify;
          }
          &-data {
            padding: 4px 0 15px;
            height: 58px;
            display: flex;
            align-items: center;
            font-family: PingFangSC-Regular;
            font-size: 12px;
            color: #303A51;
            .split {
              width: 2px;
              height: 14px;
              display: inline0-block;
              margin: 0 16px;
              background: #E3E6EC;
            }
            .item {
              text-align: center;
              .amount span {
                font-family: DINAlternate-Bold;
                font-size: 16px;
                color: #101724;
                letter-spacing: 0;
                text-align: center;
                line-height: 20px;
              } 
            }
          }
        }
        .submit-btn {
          width: 108px;
          height: 30px;
          font-size: 12px;
          &:target {
          border: 1px solid red;
        }
        }
        .more-btn {
          width: 108px;
          height: 30px;
          background: transparent;
        }
      }
    }
  }
</style>
