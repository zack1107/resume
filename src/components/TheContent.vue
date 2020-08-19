<template>
  <div>
    <header>
      <el-row type="flex" align="middle" justify="space-between">
        <div>
          <h1>周靖添的简历</h1>
        </div>
        <h1>
          <el-link type="primary" icon="el-icon-s-custom" href="https://www.dashsoap.com/" >我的博客</el-link>
        </h1>
      </el-row>
    </header>
    <el-row type="flex" align="middle">
      <div id="left"></div>
      <div id="right">
        <div ref="myChart" style="width:100%;height:520px" id="myChart"></div>
      </div>
    </el-row>
  </div>
</template>

<script>
import marked from "marked";
import str from "./myresume";
export default {
  name: "TheContent",
  methods: {
      setMyEchart() {
        const myChart = this.$refs.myChart;  //通过ref获取到DOM节点
        if (myChart) {
            const thisChart = this.$echarts.init(myChart);  //利用原型调取Echarts的初始化方法
            const option = {
          tooltip: {
            confine: true,
            enterable: true //鼠标是否可以移动到tooltip区域内
          },
          legend: {
            // top : '96%',                    // 图例距离顶部边距
            textStyle: {
              coFlor: "#202124",
              fontWeight: "bold",
              fontSize: "14"
            },
            data: [ "技术能力"]
          },

          calculable: true,
          color: [ "#4285F4"],
          radar: {
            name: {
              textStyle: {
                color: "#fff",
                backgroundColor: "#999",
                fontSize: "10",
                borderRadius: 3,
                padding: [3, 5]
              }
            },
            indicator: [
              { name: "Vue", max: 1 },
              { name: "Html/Css", max: 1 },
              { name: "Webpack", max: 1 },
              { name: "算法", max: 1 },
              { name: "原型设计/产品思维", max: 1 },
              { name: "Node", max: 1 },
              { name: "Linux", max: 1 },
              
            ],
            radius: 80
          },
          series: [
            {
              type: "radar",
              data: [
         
                {
                  value: [
                    0.80,0.75,0.57,0.55,0.52,0.3,0.5
                  ],
                  name: "技术能力"
                }
              ]
            }
          ]
        }; 
            thisChart.setOption(option);  //将编写好的配置项挂载到Echarts上
            window.addEventListener("resize", function() {
                thisChart.resize();  //页面大小变化后Echarts也更改大小
            });
        }
      }
    },
  mounted: function() {
      this.setMyEchart();

    this.$nextTick(function() {
      document.getElementById("left").innerHTML = marked(str);
    });
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

*{
  /* font-family: "Indie Flower", cursive; */
}


header {
  position: sticky;
  top: 0;
  padding: 0 5%;
  background: rgba(255, 255, 255, 0.8);
  z-index: 1;
  box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
}
#left {
  display: inline-block;
  max-width: 50%;
}
#right {
  display: inline-block;
  min-width: 50%;
}
</style>
