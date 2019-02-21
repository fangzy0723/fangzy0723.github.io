# vue使用Echarts图表

### 1、全局引用事例

- #### 安装echarts

```
npm install echarts --save
```

- #### main.js 全局引用

```js
// 引入echarts
import echarts from 'echarts'
Vue.prototype.$echarts = echarts
```

- #### test.vue 页面部分

```vue
<div id="myChartbar" :style="{width: '600px', height: '600px'}"></div>
```

- #### test.vue js部分

```js
export default {
  name: 'test',
  data () {
    return {
    }
  },
  mounted(){
    this.drawLine();
  },
  methods: {
    drawLine(){
        let myChartbar = this.$echarts.init(document.getElementById('myChartbar'))
        // 绘制图表
        myChartbar.setOption({
            title: { text: '在Vue中使用echarts柱状图示例' },
            tooltip: {},
            xAxis: {
                data: ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
            },
            yAxis: {},
            series: [{
                name: '销量',
                type: 'bar',
                data: [5, 20, 36, 10, 10, 20]
            }]
        });
    }
  }
}
```



### 2、按需引入示例

- #### test.vue 页面部分

```vue
<div id="myChartbar" :style="{width: '600px', height: '600px'}"></div>
<div id="myChartPie" :style="{width: '600px', height: '600px'}"></div>
<div id="myChartLine" :style="{width: '600px', height: '600px'}"></div>
```

- #### test.vue js部分

  > [按需引入参考](https://github.com/apache/incubator-echarts/blob/master/index.js)

```js
	// 引入基本模板
    import echarts from 'echarts/lib/echarts'
    // 引入柱状图组件
    import('echarts/lib/chart/bar')
    // 引入饼图组件
    import('echarts/lib/chart/pie')
    // 引入折线图组件
    import('echarts/lib/chart/line')

    // 引入提示框和title组件
    import('echarts/lib/component/tooltip')
    import('echarts/lib/component/title')
    export default {
        name: 'test',
        data() {
            return {
            }
        },
        mounted() {
            this.drawBar();
            this.drawLine()
            this.drawPie()
        },
        methods: {
            drawBar() {
                // 基于准备好的dom，初始化echarts实例
                let myChartbar = echarts.init(document.getElementById('myChartbar'))
                // 绘制图表
                myChartbar.setOption({
                    title : {
                        text: '在Vue中使用echarts柱状图示例',
                        subtext: '测试用例',
                        x:'center'
                    },
                    tooltip : {
                        trigger: 'item',
                        formatter: "{a} <br/>{b} : {c}"
                    },
                    xAxis: {
                        data: ["衬衫", "羊毛衫", "雪纺衫", "裤子", "高跟鞋", "袜子"]，
                        axisLabel:{
                            interval:0,//横轴信息全部显示
                            rotate:-15,//-15度角倾斜显示
                        }
                    },
                    yAxis: {},
                    series: [{
                        name: '销量',
                        type: 'bar',
                        data: [5, 20, 36, 10, 10, 20]
                    }]
                });
            },
            drawLine() {
                // 基于准备好的dom，初始化echarts实例
                let myChartLine = echarts.init(document.getElementById('myChartLine'))
                // 绘制图表
                myChartLine.setOption({
                    title : {
                        text: '在Vue中使用echarts折线图示例',
                        subtext: '测试用例',
                        x:'center'
                    },
                    tooltip : {
                        trigger: 'item',
                        formatter: "{a} <br/>{b} : {c}"
                    },
                    xAxis: {
                        type: 'category',
                        data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']，
                        axisLabel:{
                            interval:0,//横轴信息全部显示
                            rotate:-15,//-15度角倾斜显示
                        }
                    },
                    yAxis: {
                        type: 'value'
                    },
                    series: [{
                        data: [820, 932, 901, 934, 1290, 1330, 1320],
                        type: 'line'
                    }]
                });
            },

            drawPie() {
                // 基于准备好的dom，初始化echarts实例
                let myChartPie = echarts.init(document.getElementById('myChartPie'))
                let data = [{name: "张三", value: 27568},
                            {name: "丽萨", value: 91767},
                            {name: "里斯", value: 68436},
                            {name: "拉妲", value: 2993},
                            {name: "苏黎世", value: 59130}]

                // 绘制图表
                myChartPie.setOption({
                    title : {
                        text: '在Vue中使用echarts饼图示例',
                        subtext: '测试用例',
                        x:'center'
                    },
                    tooltip : {
                        trigger: 'item',
                        formatter: "{a} <br/>{b} : {c} ({d}%)"
                    },
                    legend: {
                        type: 'scroll',
                        orient: 'vertical',
                        right: 10,
                        top: 20,
                        bottom: 20,
                    },
                    series : [
                        {
                            name: '姓名',
                            type: 'pie',
                            radius : '55%',
                            center: ['40%', '50%'],
                            data: data,
                            itemStyle: {
                                emphasis: {
                                    shadowBlur: 10,
                                    shadowOffsetX: 0,
                                    shadowColor: 'rgba(0, 0, 0, 0.5)'
                                }
                            }
                        }
                    ]
                });
            },
        }
    }
```

