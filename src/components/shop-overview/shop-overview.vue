<template>
  <div class="overview-bg" >
    <div class="header">
      <i class="icon-arrow_lift" @click></i>
      <p>店铺概览</p>
    </div>
    <div class="title">
      <span class="shopkeeper">Hi~ big Boss</span>
      <span class="shopname">星巴克咖啡 1F 1001</span>
    </div> 
    <div class="content-wrapper" ref="contentWrapper">
      <div>
        <!--更新时间-->
        <div class="time"> 16:00更新 </div>
        <!--获客率-->
        <div class="rate">
          <div class="now">
            <div>38.7%</div>
            <span>本层获客率</span>
          </div>
          <div class="all">
            <div>78.5%</div>
            <span>商圈获客率</span>
          </div>
        </div>
        <!--时段客流 条形统计图-->
        <div class="passenger-flow">
          <div class="title">
            <div class="details">时段客流</div>
            <div class="update">16:00更新</div>
          </div>
          <!--条形图-->
          <div class="echarts">
            <IEcharts :option="bar" @ready="onReady" @click="onClick"></IEcharts>
          </div>
        </div>
        <!--驻留时长  折线统计图-->
        <div class="resident-time">
          <div class="title">
            <div class="details">驻留时长（分钟）</div>
            <div class="update">16:00更新</div>
          </div>
          <!--条形图-->
          <div class="echarts">
            <IEcharts :option="line" @ready="onReady" @click="onClick"></IEcharts>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script type="text/ecmascript">
  import IEcharts from 'vue-echarts-v3/src/full.js';
  import BScroll from 'better-scroll';
  
   export default {
    name: 'view',
    components: {
      IEcharts
    },
    props: {
    },
    data() {
      return {
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
              name : '时段',
              nameLocation: 'end',
              nameTextStyle: {
                color: '#72fffd',
                fontSize: 22
              },
              data : ['10-11', '11-12', '12-13', '13-14', '14-15', '15-16', '16-17','17-18', '18-19', '19-20', '20-21', '21-22'],
              axisTick: { // 保证刻度线和标签对齐
                alignWithLabel: true
              },
              axisLabel: {
                color: '#6199ea',
                fontSize: 22, 
                rotate: 45
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
              data:[10, 52, 200, 334, 390, 330, 220, 45, 56, 76, 357, 260]
            }
          ]
        },
        // 折线
        line: {
            animation: false,
            title: {
                left: 'center',
                text: '触屏 tooltip 和 dataZoom 示例',
                subtext: '"tootip" and "dataZoom" on mobile device',
            },
            legend: {
                top: 'bottom',
                data:['意向']
            },
            tooltip: {
                triggerOn: 'none',
                position: function (pt) {
                    return [pt[0], 130];
                }
            },
            toolbox: {
                left: 'center',
                itemSize: 25,
                top: 55,
                feature: {
                    dataZoom: {
                        yAxisIndex: 'none'
                    },
                    restore: {}
                }
            },
            xAxis: {
                type: 'time',
                // boundaryGap: [0, 0],
                axisPointer: {
                    value: '2016-10-7',
                    snap: true,
                    lineStyle: {
                        color: '#004E52',
                        opacity: 0.5,
                        width: 2
                    },
                    label: {
                        show: true,
                        backgroundColor: '#004E52'
                    },
                    handle: {
                        show: true,
                        color: '#004E52'
                    }
                },
                splitLine: {
                    show: false
                }
            },
            yAxis: {
                type: 'value',
                splitLine: {
                    show: false
                },
                axisLabel: {
                    inside: true,
                    formatter: '{value}\n'
                },
                z: 10
            },
            grid: {
                top: 20,
                left: 15,
                right: 15
            },
            dataZoom: [{
                type: 'inside',
                throttle: 50
            }],
            series: [
                {
                    name:'模拟数据',
                    type:'line',
                    smooth: true,
                    symbol: 'circle',
                    symbolSize: 5,
                    sampling: 'average',
                    itemStyle: {
                        normal: {
                            color: '#8ec6ad'
                        }
                    },
                    stack: 'a',
                    areaStyle: {
                        normal: {
                            color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [{
                                offset: 0,
                                color: '#8ec6ad'
                            }, {
                                offset: 1,
                                color: '#ffe'
                            }])
                        }
                    },
                    data: [1,2,3]
                },
                {
                    name:'模拟数据',
                    type:'line',
                    smooth:true,
                    stack: 'a',
                    symbol: 'circle',
                    symbolSize: 5,
                    sampling: 'average',
                    itemStyle: {
                        normal: {
                            color: '#d68262'
                        }
                    },
                    areaStyle: {
                        normal: {
                            color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [{
                                offset: 0,
                                color: '#d68262'
                            }, {
                                offset: 1,
                                color: '#ffe'
                            }])
                        }
                    },
                    data: [3,4,5]
                }
        
            ]
        }
      }
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
      onReady(instance) {
        console.log(instance);
      },
      _initScroll() {
        this.contentScroll = new BScroll(this.$refs.contentWrapper, {
          click: true // 设置后可以点击，默认派发了一个点击事件
        });
      }
    }
  };
</script>

<style lang="scss" scoped>
 @import '../../assets/hotcss/px2rem.scss';
  .overview-bg {
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
      /*获客率*/
      .rate {
        display: flex;
        width: 100%;
        /*height: px2rem(185);*/
        color: #84fffd;
        text-align: center;
        padding: px2rem(46) 0;
        box-sizing: border-box;
        .now, .all {
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
      /*时段客流*/
      .passenger-flow {
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
      /*驻留时长*/
      .resident-time {
        width: 100%;
        height: px2rem(570);
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
          width: 100%;
          height: 100%;
          /*padding: 0 px2rem(25);*/
          box-sizing: border-box;
        }
      }
    }
  }
  
</style>

