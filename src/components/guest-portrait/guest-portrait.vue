<template>
  <div class="container-bg" >
    <div class="header">
      <i class="icon-arrow_lift" @click></i>
      <p>客群画像</p>
    </div>
    <div class="title">
      <span class="shopkeeper">Hi~ big Boss</span>
      <span class="shopname">星巴克咖啡 1F 1001</span>
    </div> 
    <div class="content-wrapper" ref="contentWrapper">
      <div>
        <!--性别比例-->
        <div class="gender">
          <div class="male">
            <div>38.9%</div>
            <span>男性</span>
          </div>
          <div class="female">
            <div>78.2%</div>
            <span>女性</span>
          </div>
        </div>
        <!--年龄分布 折线统计图-->
        <div class="age-distribution">
          <div class="title">
            <div class="details">年龄分布</div>
          </div>
          <!--折线图-->
          <div class="echarts">
            <IEcharts :option="line" ></IEcharts>
          </div>
        </div>
        <!--学历分布  饼状统计图-->
        <div class="education">
          <div class="title">
            <div class="details">学历分布</div>
          </div>
          <!--饼状图-->
          <div class="echarts">
            <IEcharts :option="pie" ></IEcharts>
          </div>
        </div>
        <!--职业分布  条形图-->
        <div class="occupational-distribution">
          <div class="title">
            <div class="details">职业分布</div>
          </div>
          <div class="echarts">
            <IEcharts :option="bar" ></IEcharts>
          </div>
        </div>
        <!--私家车拥有情况 -->
        <div class="private-car">
          <div class="title">
            <div class="details">私家车拥有情况</div>
          </div>
          <div class="has-car">
            <div>38.9%</div>
            <span>有车</span>
          </div>
          <div class="no-car">
            <div>78.2%</div>
            <span>无车</span>
          </div>
        </div>
        <!--消费能力-->
        <div class="consumption-capacity">
          <div class="title">
            <div class="details">消费能力</div>
          </div>
          <!--饼图-->
          <div class="echarts">
            <IEcharts :option="pie2"></IEcharts>
          </div>
        </div>
        <!--逛店偏好-->
        <div class="shop-preference">
          <div class="title">
            <div class="details">逛店偏好</div>
          </div>
          <!--条图形-->
          <div class="echarts">
            <IEcharts :option="bar2"></IEcharts>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script type="text/ecmascript">
  import IEcharts from 'vue-echarts-v3/src/full.js';
  import BScroll from 'better-scroll';
  import 'echarts/lib/chart/line';
  
  export default {
    name: 'view',
    components: {
      IEcharts
    },
    props: {
    },
    data() {
      return {
        chooseType: 1,
        // 折线
        line: {
          grid: {
            left: '2%',
            bottom: '3%',
            containLabel: true 
          },
          xAxis: {
              show: true,
              type: 'category',
              name: '年龄',
              nameLocation: 'end',
              nameTextStyle: {
                color: '#72fffd',
                fontSize: 22
              },
              axisLabel: {
                color: '#6199ea',
                fontSize: 22
              },
              axisLine: {
                lineStyle: {color: '#2b5f6f'}
              },
              boundaryGap: false, // 坐标轴两边留白策略，类目轴和非类目轴的设置和表现不一样。
              data: ['<18', '18-22', '23-27', '28-32', '33-37', '38-42', '43-47', '>48']
          },
          yAxis: {
              show: true,
              type: 'value',
              name: '人数',
              nameLocation: 'end',
              nameTextStyle: {
                color: '#72fffd',
                fontSize: 22
              },
              min: 0,
              max: 400,
              splitNumber: 2, // 坐标轴的分割段数
              axisLabel: {
                color: '#6199ea',
                fontSize: 22
              },
              axisLine: {
                lineStyle: {color: '#2b5f6f'}
              },
              splitLine: {
                lineStyle: {
                  color: '#29426d'
                }
              }
          },
          series: [
            {
              name:'模拟数据',
              type:'line',
              symbol: 'circle', // 折线拐点是 圆
              sampling: 'average', // 取过滤点的平均值
              itemStyle: { // 折线拐点标志的样式。
                normal: {
                  color: 'rgb(42, 209, 207)'
                }
              },
              areaStyle: { // 区域填充样式。
                normal: {
                  // 线性渐变，前四个参数分别是 x0, y0, x2, y2, 范围从 0 - 1，相当于在图形包围盒中的百分比，如果 globalCoord 为 `true`，则该四个值是绝对的像素位置
                  color: {
                    type: 'linear',
                    x: 0,
                    y: 0,
                    x2: 0,
                    y2: 1,
                    colorStops: [{
                        offset: 0, color: 'rgba(34, 145, 146, .9)' // 0% 处的颜色
                    }, {
                        offset: 1, color: 'rgba(25, 71, 110, .1)' // 100% 处的颜色
                    }],
                    globalCoord: false // 缺省为 false
                  }
                }
              },
              data: [200, 324, 200, 200, 146, 180, 220,360]
            }
          ] 
        },
        // 饼状
        pie :{
          tooltip : {
              trigger: 'item',
              formatter: "{a} <br/>{b} : {c} ({d}%)"
          },
          series : [
            {
              name: '学历分布',
              type: 'pie',
              radius : '75%',
              center: ['50%', '60%'],
              data:[
                  {value:125, name:'高中及以下 12.5%'},
                  {value:249, name:'专科 24.9%'},
                  {value:549, name:'本科 54.9%'},
                  {value:389, name:'硕士及以上 38.9%'}
              ],
              color: ['#ee619c', '#36a0c2', '#f8df74', '#2ad1cf'],
              label:{
                normal:{
                  fontSize: 24,
                  color: '#fff'
                }
              },
              labelLine: {
                normal: {
                  length: 40,
                  length2: 60,
                  lineStyle: {
                    color: '#2ad1cf'
                  }
                }
              },
              itemStyle: {
                emphasis: {
                    shadowBlur: 10,
                    shadowOffsetX: 0,
                    shadowColor: 'rgba(0, 0, 0, 0.5)'
                }
              }
            }
          ],
          markPoint: {
            symbolRotate: 50,
            label: {
              normal: {
                position: 'top',
                distance: 20,
                rotate: -45
              }
            }
          }
        },
        bar: {
          color: ['#54d7ff','#72fffd'],
          tooltip : {
            trigger: 'axis',
            axisPointer : {            // 坐标轴指示器，坐标轴触发有效
              type : 'shadow'        // 默认为直线，可选为：'line' | 'shadow'
            }
          },
          grid: {
            left: '2%',
            bottom: '3%',
            containLabel: true 
          },
          xAxis : [
            { 
              show: true,
              type : 'category',
              name : '职业',
              nameLocation: 'end',
              nameTextStyle: {
                color: '#72fffd',
                fontSize: 22
              },
              data : ['公务员', '技术人员', '企业管理者', '个体经营', '服务人员'],
              axisTick: { // 保证刻度线和标签对齐
                alignWithLabel: true
              },
              axisLabel: {
                color: '#6199ea',
                fontSize: 22
              },
              axisLine: {
                lineStyle: {color: '#2b5f6f'}
              },
              boundaryGap: true
            }
          ],
          yAxis : [
            {
              show: true,
              type : 'value',
              min: 0,
              max: 400,
              splitNumber: 2, // 坐标轴的分割段数
              name : '人数',
              nameLocation: 'end',
              nameTextStyle: {
                color: '#72fffd',
                fontSize: 22
              },
              axisLabel: { // 坐标轴刻度标签
                color: '#6199ea',
                fontSize: 22
              },
              axisLine: {
                lineStyle: {color: '#2b5f6f'}
              },
              splitLine: {show: false}
            }
          ],
          series : [
            {
              name:'直接访问',
              type:'bar',
              barWidth: '30%',
              itemStyle: {
                normal: {
                  color: function (val) {
                    return val.dataIndex % 2 ? '#72fffd' : '#54d7ff'
                  }
                }
              },
              data:[100, 140, 160, 250, 210]
            }
          ]
        },
        // pie2
        pie2 :{
          tooltip : {
              trigger: 'item',
              formatter: "{a} <br/>{b} : {c} ({d}%)"
          },
          series : [
            {
              name: '消费能力',
              type: 'pie',
              radius : '75%',
              center: ['60%', '60%'],
              data:[
                  {value:99, name:'低 9.9%'},
                  {value:229, name:'中低 22.9%'},
                  {value:273, name:'中 27.3%'},
                  {value:225, name:'中高 22.5%'},
                  {value:189, name:'高 18.9%'}
              ],
              color: ['#ee619c', '#36a0c2', '#f8df74', '#2ad1cf', '#6664ed'],
              label:{
                normal:{
                  fontSize: 24,
                  color: '#fff'
                }
              },
              labelLine: {
                normal: {
                  length: 40,
                  length2: 60,
                  lineStyle: {
                    color: '#2ad1cf'
                  }
                }
              },
              itemStyle: {
                emphasis: {
                    shadowBlur: 10,
                    shadowOffsetX: 0,
                    shadowColor: 'rgba(0, 0, 0, 0.5)'
                }
              }
            }
          ],
          markPoint: {
            symbolRotate: 50,
            label: {
              normal: {
                position: 'top',
                distance: 20,
                rotate: -45
              }
            }
          }
        },
        // bar2
        bar2: {
          color: ['#54d7ff','#72fffd'],
          tooltip : {
            trigger: 'axis',
            axisPointer : {            // 坐标轴指示器，坐标轴触发有效
              type : 'shadow'        // 默认为直线，可选为：'line' | 'shadow'
            }
          },
          grid: {
            left: '2%',
            bottom: '3%',
            containLabel: true 
          },
          xAxis : [
            { 
              show: false,
              type : 'value',
              data : ['公务员', '技术人员', '企业管理者', '个体经营', '服务人员'],
              boundaryGap: true
            }
          ],
          yAxis : [
            {
              type: 'category',
              data: ['5·休闲-电影院', '4·休闲-KTV', '3·餐饮-川菜', '2·餐饮-饮品', '1·零售-服饰'],
              axisLine: {
                lineStyle: {color: 'transparent'}
              },
              axisLabel: {
                color: '#6199ea',
                fontSize: 22,
                margin: 50
              }
            }
          ],
          series : [
            {
              name:'直接访问',
              type:'bar',
              barWidth: '30%',
              itemStyle: {
                normal: {
                  color: function (val) {
                    return val.dataIndex % 2 ? '#72fffd' : '#54d7ff'
                  },
                  color: {
                    type: 'linear',
                    x: 1,
                    y: 0,
                    x2: 0,
                    y2: 0,
                    colorStops: [{
                        offset: 0, color: 'rgba(117, 227, 255, .8)'  // 0% 处的颜色
                    }, {
                        offset: 1, color: 'rgba(64, 214, 222, .8)' // 100% 处的颜色
                    }],
                    globalCoord: false // 缺省为 false
                  }
                }
              },
              data:[100, 140, 160, 210, 250]
            }
          ]
        }
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
      doRandom() {
        const that = this;
        let data = [];
        for (let i = 0, min = 5, max = 99; i < 6; i++) {
          data.push(Math.floor(Math.random() * (max + 1 - min) + min));
        }
        that.loading = !that.loading;
        that.bar.series[0].data = data;
      },
      _initScroll() {
        this.contentScroll = new BScroll(this.$refs.contentWrapper, {
          click: true // 设置后可以点击，默认派发了一个点击事件
        });
      },
      addActive (type, event) {
//      better-scroll中event._constructed===true  pc下不会触发两次click
        if (!event._constructed) {
          return;
        }
        this.chooseType = type;
        console.log(1);
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
      /*更新时间*/
      .time {
        margin: 0 auto;
        width: px2rem(214);
        height: px2rem(30);
        line-height: px2rem(30);
        color: #6199ea;
        font-size: px2rem(24);
        text-align: center;
        /*background: linear-gradient(left, rgba(26,61,106,0) 0%, rgba(26,61,106,1) 7%, rgba(26,61,106,0) 93%);*/
        background: linear-gradient(to right, transparent , #216ba0, transparent);      
      }
      /* 男女比例 */
      .gender, .private-car {
        display: flex;
        width: 100%;
        /*height: px2rem(185);*/
        color: #84fffd;
        text-align: center;
        padding: px2rem(46) 0;
        box-sizing: border-box;
        .male, .female {
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
      /*年龄分布、学历分布、职业分布、拥有私家车*/
      .age-distribution, .education, .occupational-distribution, .private-car, .consumption-capacity, .shop-preference {
        width: 100%;
        height: px2rem(550);
        padding: px2rem(45) 0;
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
            margin-left: px2rem(12);
            padding-left: px2rem(18);
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
            margin-right: px2rem(26);
            font-size: px2rem(28);
            color: #6199ea;
          }
        }
        .echarts {
          width: px2rem(750);
          height: px2rem(400);
          /*padding: 0 px2rem(25);*/
          box-sizing: border-box;
        }
      }
      .btns {
        font-size: 0;
        text-align: center;
        padding-bottom: px2rem(76);
        div {
          position: relative;
          display: inline-block;
          width: px2rem(120);
          height: px2rem(70);
          border-radius: px2rem(4);
          border: 1px solid #1a346b;
          line-height: px2rem(70);
          text-align: center;
          color: #6199ea;
          font-size: px2rem(22);
          background: #20407a;
        }
        .prev {
          left: px2rem(4);
          z-index: 10;
        }
        .active {
          background: #3359a4;
          z-index: 11;
        }
      }
    }
  }
  
</style>

