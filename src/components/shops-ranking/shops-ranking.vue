<template>
  <div class="container-bg" >
    <div class="header">
      <i class="icon-arrow_lift" @click></i>
      <p>商铺排行</p>
    </div>
    <div class="title">
      <span class="shopkeeper">Hi~ big Boss</span>
      <span class="shopname">星巴克咖啡 1F 1001</span>
    </div> 
    <div class="content-wrapper" ref="contentWrapper">
      <div>
        <div class="btns">
          <div class="all " :class="{'active':chooseItem===1}" @click="isActive(1, $event)">全部</div>
          <div class="yetai" :class="{'active':chooseItem===2}" @click="isActive(2, $event)">本业态</div>
          <div class="louceng" :class="{'active':chooseItem===3}" @click="isActive(3, $event)">本楼层</div>
        </div>
        <!-- 客流量 -->
        <div class="passenger-flow">
          <div class="title">
            <div class="details">客流量</div>
            <div class="update">16:00更新</div>
          </div>
          <div class="description">
            <div class="today">
              <div>38</div>
              <span>今日排名</span>
            </div>
            <div class="yesterday">
              <div>40</div>
              <span>昨日排名</span>
            </div>
          </div>
        </div>
        
        <!--平均驻留时长-->
        <div class="resident-time">
          <div class="title">
            <div class="details">平均驻留时长</div>
            <div class="update">16:00更新</div>
          </div>
          <div class="description">
            <div class="today">
              <div>22</div>
              <span>今日排名</span>
            </div>
            <div class="yesterday">
              <div>18</div>
              <span>昨日排名</span>
            </div>
          </div>
        </div>
        
        <!--获客坪效-->
        <div class="passenger-level">
          <div class="title">
            <div class="details">获客坪效</div>
            <div class="update">16:00更新</div>
          </div>
          <div class="description">
            <div class="today">
              <div>23</div>
              <span>今日排名</span>
            </div>
            <div class="yesterday">
              <div>21</div>
              <span>昨日排名</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script type="text/ecmascript">
  import BScroll from 'better-scroll';
  
  export default {
    props: {
    },
    data() {
      return {
        chooseItem: 1
      };
    },
    created () {
      // 异步更新DOM，数据改变的时候，DOM并没有变化，这里scroll计算的高度就有问题
      this.$nextTick(() => {
        this._initScroll();
        console.log(this.$refs.contentWrapper);
      });
    },
    methods: {
      _initScroll() {
        this.contentScroll = new BScroll(this.$refs.contentWrapper, {
          click: true // 设置后可以点击，默认派发了一个点击事件
        });
      },
      isActive (item, event) {
//      better-scroll中event._constructed===true  pc下不会触发两次click
        if (!event._constructed) {
          return;
        }
        this.chooseItem = item;
      }
    },
    computed: {
    }
  };
</script>

<style lang="scss" scoped>
 @import '../../assets/hotcss/px2rem.scss';
  .container-bg {
    position: absolute;
    top: 0;
    left: 0;
    bottom: px2rem(110);
    width: 100%;
    background: #102d5c;
    /*padding-bottom: 110px;*/
    /*头部*/
    .header {
      position: relative;
      width: 100%;
      height: px2rem(126);
      color: #fff;
      .icon-arrow_lift {
        position: absolute;
        top: px2rem(30);
        left: 0;
        display: inline-block;
        padding: px2rem(30);
        font-size: px2rem(36);
      }
      p {
        position: absolute;
        top: px2rem(30);
        left: 0;
        display: inline-block;
        margin:0 auto;
        width: 100%;
        line-height: px2rem(96);
        text-align: center;
      }
    }
    /*店主 店名 信息*/
    &>.title {
      width: 100%;
      height: px2rem(40);
      margin-top: px2rem(26);
      background-color: #25577d;
      line-height: px2rem(40);
      color: #72fffd;
      font-size: px2rem(24);
      .shopkeeper {
        float: left;
        margin-left: px2rem(20);
      }
      .shopname {
        float: right;
        margin-right: px2rem(20);
      }
    }
    .content-wrapper {
      position: absolute;
      top: px2rem(192);
      bottom: 0;
      width: 100%;
      overflow: hidden;
      /* tabs */
      .btns {
        display: flex;
        margin: px2rem(30) auto 0;
        padding: px2rem(12) 0;
        box-sizing: border-box;
        width: px2rem(622);
        height: px2rem(70);
        background: #1f4079;
        font-size: px2rem(26);
        color: #6199ea;
        border-radius: px2rem(5);
        text-align: center;
        div {
          flex: 1;
          line-height: px2rem(50);
        }
        .all, .yetai {
          border-right: 1px solid #1a346b;
        }
        .active {
          height: px2rem(70);
          line-height: px2rem(70);
          margin-top: px2rem(-12);
          background: #3259a1;
          border-radius: px2rem(5);
        }
      }
      /*客流量 、 驻留时长 、 获客坪效*/
      .passenger-flow, .resident-time, .passenger-level {
        margin: px2rem(30) auto 0;
        width: px2rem(630);
        height: px2rem(264);
        /*padding: px2rem(45) 0;*/
        box-sizing: border-box;
        .title {
          width: 100%;
          height: px2rem(40);
          .details {
            position: relative;
            width: px2rem(265);
            height: px2rem(40);
            line-height: px2rem(40);
            font-size: px2rem(28);
            color: #84fffd;
            background: #24567b;
            float: left;
            &:after {
              content: '';
              display: block;
              position: absolute;
              top: 0;
              right: px2rem(-20);
              width: px2rem(50);
              height: px2rem(40);
              transform: skewX(30deg);
              background: #24567b;
            }
          }
          .update {
            float: right;
            font-size: px2rem(28);
            color: #6199ea;
          }
        }
        .description {
          margin: 0 auto;
          width: px2rem(630);
          height: px2rem(222);
          padding: px2rem(50) 0;
          box-sizing: border-box;
          background: #1e4372;
          display: flex;
          text-align: center;
          color: #84fffd;
          .today, .yesterday {
            flex: 1;
            div {
              font-size: px2rem(60);
              margin-bottom: px2rem(6);
            }
            span {
              font-size: px2rem(28);
            }
          }
        }
      }
    }
  }
</style>

