<template>
  <div>
    <div class="analysis-data">
      <p class="analysis-data-title">数据概况</p>
      <div class="analysis-data-info">
        <div class="analysis-data-title_1">{{infoData.a}}</div>
        <div class="analysis-data-title_2">{{infoData.b}}</div>
        <div class="analysis-data-title_3">{{infoData.c}}</div>
      </div>
    </div>
    <p class="analysis-data-title">销量走势</p>
    <div id="analysis-graph">

    </div>
  </div>
</template>

<script>
import * as echarts from "echarts";
export default {
  data() {
    return {

        infoData:{
            a:0,
            b:0,
            c:0,
        }
    };
  },
  methods: {
    mGetDate() {
      var date = new Date();
      var year = date.getFullYear();
      var month = date.getMonth() + 1;
      var d = new Date(year, month, 0);
      return d.getDate();
    },
    generateMonthList() {
      let days = this.mGetDate();
      return Array.apply(null, { length: days }).map((_, index) => {
        return index + 1;
      });
    },
    generateTestData() {
      let days = this.mGetDate();
      return Array.apply(null, { length: days }).map((_, index) => {
        return (Math.random() * 1000).toFixed(1);
      });
    },
    initGraph() {
      let chartDom = document.getElementById("analysis-graph");
      let myChart = echarts.init(chartDom);
      let option;
    
      option = {
        xAxis: {
          type: "category",
          data: this.generateMonthList(),
        },
        yAxis: {
          type: "value",
        },
        tooltip: {
          trigger: "axis",
          showContent: false
        },
        legend: {
          data: ["一", "二", "三"],
          y: "bottom",
        },
        grid: {
          left: "10%", //因旋转导致名字太长的类目造成遮蔽，可以配合这两个属性
          bottom: "10%", // 分别表示：距离左边距和底部的距离，具体数值按实际情况调整
        },
        dataZoom: [
          {
            type: "inside",
            realtime: true, //拖动滚动条时是否动态的更新图表数据
            height: 0, //滚动条高度
            start: 70, //滚动条开始位置（共100等份）
            end: 100, //结束位置（共100等份）
          },
        ],
        series: [
          {
            name: "一",
            data: this.generateTestData(),
            type: "line",
            smooth: true,
          },
          {
            name: "二",
            data: this.generateTestData(),
            type: "line",
            smooth: true,
          },
          {
            name: "三",
            data: this.generateTestData(),
            type: "line",
            smooth: true,
          },
        ],
      };
      var self = this;
      myChart.on("updateAxisPointer", function (event) {
        // console.log(option.series)
        let index = event.dataIndex
        self.infoData.a=option.series[0].data[index]
        self.infoData.b=option.series[1].data[index]
        self.infoData.c=option.series[2].data[index]
        // this.$set(infoData,a,'123')
        // console.log(event.dataIndex); //这里根据param填写你的跳转逻辑
      });
      option && myChart.setOption(option);
    },
  },
  mounted() {
    this.initGraph();
  },
};
</script>

<style scoped lang="scss">
.analysis-data-title {
  text-align: left;
}
.analysis-data-info {
  display: flex;
  justify-content: space-around;
  & > div {
    height: 50px;
    width: 60px;
    background-color: #cfcfcf;
    padding: 0 10px;
  }
}
#analysis-graph {
  height: 300px;
  margin-top:-50px;
}
</style>