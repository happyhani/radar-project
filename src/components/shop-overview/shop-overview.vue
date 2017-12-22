<template>
  <div class="container-bg" >
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
            <IEcharts :option="bar" ></IEcharts>
          </div>
        </div>
        <!--驻留时长  折线统计图-->
        <div class="resident-time">
          <div class="title">
            <div class="details">驻留时长（分钟）</div>
            <div class="update">16:00更新</div>
          </div>
          <!--折线图-->
          <div class="echarts">
            <IEcharts :option="line" ></IEcharts>
          </div>
        </div>
        <!--客流走向分析  桑基图-->
        <div class="passenger-trend">
          <div class="title">
            <div class="details">客流走向分析</div>
            <div class="update">16:00更新</div>
          </div>
          <!--桑基图 客流导入-->
          <p>客流导入 TOP5</p>
          <div class="echarts">
            <IEcharts :option="sankey1" ></IEcharts>
          </div>
          <!--店铺占比-->
          <div class="shop-statistics">
            <ul>
            	<li class="one">
            	  <p>12.9%</p>
            	  <p>店铺一</p>
            	  <div></div>
            	</li>
            	<li class="one">
                <p>12.9%</p>
                <p>店铺二</p>
                <div></div>
              </li>
              <li class="one">
                <p>12.9%</p>
                <p>店铺三</p>
                <div></div>
              </li>
              <li class="one">
                <p>12.9%</p>
                <p>店铺四</p>
                <div></div>
              </li>
              <li class="one">
                <p>12.9%</p>
                <p>店铺五</p>
                <div></div>
              </li>
            </ul>
          </div>
          <!--桑基图  客流导出-->
          <p>客流导出 TOP5</p>
          <div class="echarts">
            <IEcharts :option="sankey2" ></IEcharts>
          </div>
          <!--店铺占比-->
          <div class="shop-statistics">
            <ul>
              <li class="one">
                <p>12.9%</p>
                <p>店铺一</p>
                <div></div>
              </li>
              <li class="one">
                <p>12.9%</p>
                <p>店铺二</p>
                <div></div>
              </li>
              <li class="one">
                <p>12.9%</p>
                <p>店铺三</p>
                <div></div>
              </li>
              <li class="one">
                <p>12.9%</p>
                <p>店铺四</p>
                <div></div>
              </li>
              <li class="one">
                <p>12.9%</p>
                <p>店铺五</p>
                <div></div>
              </li>
            </ul>
          </div>
        </div>
        <!--获客坪效 条形统计图-->
        <div class="passenger-level">
          <div class="title">
            <div class="details">获客坪效</div>
            <div class="update">16:00更新</div>
          </div>
          <!--条形图-->
          <div class="echarts">
            <IEcharts :option="bar2" ></IEcharts>
          </div>
        </div>
        <!--按钮-->
        <div class="btns">
          <div class="prev" :class="{'active':chooseType===1}" @click="addActive(1, $event)">上一周</div>
          <div class="now" :class="{'active':chooseType===2}" @click="addActive(2, $event)">本周</div>
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
          grid: {
            left: '2%',
            bottom: '3%',
            containLabel: true 
          },
          xAxis: {
              show: true,
              type: 'category',
              name: '时长',
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
              data: ['<1', '1-3', '3-5', '5-10', '10-20', '20-30', '>30']
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
              data: [200, 324, 200, 200, 146, 200, 400]
            }
          ] 
        },
        sankey1: {
          tooltip: {
            trigger: 'item',
            triggerOn: 'mousemove'
          },
          series: [
            {
              type: 'sankey',
              right: '10%',
              layout:'none',
              data: [
                { "name":"left01", 
                  "itemStyle": {"normal": {"color": "#54d7ff"}},
                  "label": {"normal": {"color": "transparent"}}
                },
                {"name":"left02", 
                  "itemStyle": {"normal":{"color": "#e1b779"}},
                  "label": {"normal": {"color": "transparent"}}
                },
                {"name":"left03", 
                  "itemStyle": {"normal":{"color": "#927ee7"}},
                  "label": {"normal": {"color": "transparent"}}
                },
                {"name":"left04", 
                  "itemStyle": {"normal":{"color": "#61e690"}},
                  "label": {"normal": {"color": "transparent"}}
                },
                {"name":"left05", 
                  "itemStyle": {"normal":{"color": "#f19393"}},
                  "label": {"normal": {"color": "transparent"}}
                },
                {"name":"本店", 
                  "itemStyle": {"normal":{"color": "#196e8e"}},
                  "label": {"normal": {"color": "#fff","position": 'inside', "fontSize": 22}}
                }
              ],
              links: [         // 节点间的关系数据
                {
                  "source": "left01",
                  "target": "本店",  
                  "value": 20, 
                  "lineStyle":{
                    "normal":{color: "#436497"}
                  }
                },
                {"source": "left02", "target": "本店",  "value": 30, "lineStyle":{"normal":{"color":"486597"}}},
                {"source": "left03",  "target": "本店",  "value": 15, "lineStyle":{"normal":{"color":"486597"}}},
                {"source": "left04", "target": "本店",  "value": 25, "lineStyle":{"normal":{"color":"486597"}}},
                {"source": "left05",  "target": "本店",  "value": 40, "lineStyle":{"normal":{"color":"486597"}}}
              ],
              nodeWidth: 100,
              nodeGap: 15,
              itemStyle: {
                  normal: {
                      
                  }
              },
              lineStyle: {
                  normal: {
                      curveness: 0.5
                  }
              }
            }
          ]
        },
        sankey2: {
          tooltip: {
            trigger: 'item',
            triggerOn: 'mousemove'
          },
          series: [
            {
              type: 'sankey',
              right: '10%',
              layout:'none',
              data: [
                { "name":"left01", 
                  "itemStyle": {"normal": {"color": "#54d7ff"}},
                  "label": {"normal": {"color": "transparent"}}
                },
                {"name":"left02", 
                  "itemStyle": {"normal":{"color": "#e1b779"}},
                  "label": {"normal": {"color": "transparent"}}
                },
                {"name":"left03", 
                  "itemStyle": {"normal":{"color": "#927ee7"}},
                  "label": {"normal": {"color": "transparent"}}
                },
                {"name":"left04", 
                  "itemStyle": {"normal":{"color": "#61e690"}},
                  "label": {"normal": {"color": "transparent"}}
                },
                {"name":"left05", 
                  "itemStyle": {"normal":{"color": "#f19393"}},
                  "label": {"normal": {"color": "transparent"}}
                },
                {"name":"本店", 
                  "itemStyle": {"normal":{"color": "#196e8e"}},
                  "label": {"normal": {"color": "#fff","position": 'inside', "fontSize": 22}}
                }
              ],
              links: [         // 节点间的关系数据
                {
                  "source": "本店",
                  "target": "left01",  
                  "value": 20, 
                  "lineStyle":{
                    "normal":{color: "#436497"}
                  }
                },
                {"source": "本店", "target": "left02",  "value": 30, "lineStyle":{"normal":{"color":"486597"}}},
                {"source": "本店",  "target": "left03",  "value": 15, "lineStyle":{"normal":{"color":"486597"}}},
                {"source": "本店", "target": "left04",  "value": 25, "lineStyle":{"normal":{"color":"486597"}}},
                {"source": "本店",  "target": "left05",  "value": 40, "lineStyle":{"normal":{"color":"486597"}}}
              ],
              nodeWidth: 100,
              nodeGap: 15,
              itemStyle: {
                  normal: {
                      
                  }
              },
              lineStyle: {
                  normal: {
                      curveness: 0.5
                  }
              }
            }
          ]
        },
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
              show: true,
              type : 'category',
              name : '日期',
              nameLocation: 'end',
              nameTextStyle: {
                color: '#72fffd',
                fontSize: 22
              },
              data : ['周一', '周二', '周三', '周四', '周五', '周六','周日'],
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
              max: 4,
              splitNumber: 2, // 坐标轴的分割段数
              name : '坪效指数',
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
              data:[1.0, 1.2, 3.4, 2.3, 3.2, 1.4, 2.2],
              markLine : {
                data : [
                    {type : "average", name : '平均值'}
                ],
                label: {
                  normal: {
                    show: true,
                    formatter: '业态均值'
                  }
                }
              }
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
      .passenger-flow, .resident-time, .passenger-trend, .passenger-level {
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
        .shop-statistics ul{
          width: px2rem(620);
          height: px2rem(80);
          display: flex;
          margin: 0 auto;
          .one {
            flex: 1;
            p {
              text-align: center;
              font-size: px2rem(22);
              line-height: px2rem(30);
              color: #fff;
            }
            div {
              margin: px2rem(10) auto 0;
              width: px2rem(50);
              height: px2rem(5);
              background: #e1b779;
            }
          }
        }
      }
      .passenger-trend {
        width: 100%;
        height: px2rem(1150);
        padding: px2rem(45) 0;
        box-sizing: border-box;
        &>p {
          margin-top: px2rem(28);
          text-align: center;
          font-size: px2rem(22);
          color: #6199ea;
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

