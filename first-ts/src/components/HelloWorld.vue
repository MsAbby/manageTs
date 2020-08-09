<template>
  <div class="process-content">
    <div class="content" ref="content">
      <div
        id="myEcharts"
        ref="charts"
        style="width: 1000px; height: 800px"
      ></div>
      <!-- <ul>
                <li class="first-open" v-for="(item, index) in dataList" :key="index">
                    <h6>{{ item.title }}</h6>
                    <p>{{ item.content }}</p >
                    <el-button type="primary" icon="el-icon-plus" size="mini" @click="handleAddTalkContent"></el-button>
                     <el-popover
                        lacement="top"
                        width="220"
                        :ref="`popover-${item.id}`"
                        @show="handleDeleteProcess(item.id)"
                      >
                        <p><i class="el-icon-question"></i>是否将该话术删除？</p >
                        <div style="text-align: right; margin: 0">
                            <el-button size="mini" type="default" @click="handleCancel(item)">取消</el-button>
                            <el-button size="mini" type="primary" @click="handleConfirm(item)">确定</el-button>
                        </div>
                        < img slot="reference" src="@/assets/images/delete.png"/>
                    </el-popover>
                </li>
      </ul>-->
    </div>
  </div>
</template>
<script>
import echarts from "echarts";
// const echart = echarts as any;

export default {
  data() {
    return {
      dataList: [
        {
          id: 1,
          title: "开场白",
          content: "你好这里是敖德萨多多撒大所大所多很简单哈考试的哈萨克"
        }
      ],
      option: {
        series: [
          {
            type: "tree",
            left: "2%",
            right: "2%",
            top: "8%",
            bottom: "20%",
            symbol: "rect",
            orient: "vertical",
            symbolSize: [300, 200],
            edgeShape: "curve", // curve
            expandAndCollapse: true,
            label: {
              position: "top",
              rotate: -90,
              verticalAlign: "middle",
              align: "right",
              fontSize: 9
            },
            leaves: {
              label: {
                position: "bottom",
                rotate: -90,
                verticalAlign: "middle",
                align: "left"
              }
            },
            data: [
              {
                children: [
                  {
                    name: "analytics",
                    children: [
                      {
                        name: "cluster",
                        children: [
                          { name: "AgglomerativeCluster", value: 3938 },
                          { name: "CommunityStructure", value: 3812 },
                          { name: "HierarchicalCluster", value: 6714 },
                          { name: "MergeEdge", value: 743 }
                        ]
                      },
                      {
                        name: "graph",
                        children: [
                          { name: "BetweennessCentrality", value: 3534 },
                          { name: "LinkDistance", value: 5731 },
                          { name: "MaxFlowMinCut", value: 7840 },
                          { name: "ShortestPaths", value: 5914 },
                          { name: "SpanningTree", value: 3416 }
                        ]
                      },
                      {
                        name: "optimization",
                        children: [
                          {
                            name: "AspectRatioBanker",
                            value: 7074
                          }
                        ]
                      }
                    ]
                  },
                  {
                    name: "animate",
                    children: [
                      { name: "Easing", value: 17010 },
                      { name: "FunctionSequence", value: 5842 },
                      {
                        name: "interpolate",
                        children: [
                          { name: "ArrayInterpolator", value: 1983 },
                          { name: "ColorInterpolator", value: 2047 },
                          { name: "DateInterpolator", value: 1375 },
                          { name: "Interpolator", value: 8746 },
                          { name: "MatrixInterpolator", value: 2202 },
                          { name: "NumberInterpolator", value: 1382 },
                          { name: "ObjectInterpolator", value: 1629 },
                          { name: "PointInterpolator", value: 1675 },
                          { name: "RectangleInterpolator", value: 2042 }
                        ]
                      },
                      { name: "ISchedulable", value: 1041 },
                      { name: "Parallel", value: 5176 }
                    ]
                  },
                  {
                    name: "data",
                    children: [
                      {
                        name: "converters",
                        children: [
                          { name: "Converters", value: 721 },
                          { name: "DelimitedTextConverter", value: 4294 },
                          { name: "GraphMLConverter", value: 9800 },
                          { name: "IDataConverter", value: 1314 },
                          { name: "JSONConverter", value: 2220 }
                        ]
                      },
                      { name: "DataField", value: 1759 },
                      { name: "DataSchema", value: 2165 }
                    ]
                  }
                ]
              }
            ]
          }
        ]
      }

      // option: {
      //   series: [
      //     {
      //       type: "tree",
      //       data: [this.datalist],
      //       left: "2%",
      //       right: "2%",
      //       top: "8%",
      //       bottom: "20%",
      //       symbol: "emptyCircle",
      //       orient: "vertical",
      //       expandAndCollapse: true,
      //       label: {
      //         position: "top",
      //         rotate: -90,
      //         verticalAlign: "middle",
      //         align: "right",
      //         fontSize: 9
      //       },
      //       leaves: {
      //         label: {
      //           position: "bottom",
      //           rotate: -90,
      //           verticalAlign: "middle",
      //           align: "left"
      //         }
      //       },
      //       animationDurationUpdate: 750,
      //     }
      //   ]
      // }
    };
  },
  mounted() {
    this.init();
  },
  methods: {
    init() {
      const charts = echarts.init(document.getElementById("myEcharts"));
      console.log(charts);
      charts.setOption(this.option);
    }
  }
};
</script>
<style scoped lang="scss">
.process-content {
  padding: 20px;
  .card {
    background: #fff;
    width: 250px;
    height: 150px;
    border: 1px solid transparent;
    margin: 30px auto;
    border-radius: 0px;
    text-align: center;
    color: #1890ff;
    .icon {
      font-size: 22px;
      margin-top: 38px;
    }
    .text {
      font-size: 14px;
      color: #1890ff;
    }
  }
  .content {
    ul {
      margin: 0;
      padding: 0;
    }
    li {
      list-style-type: none;
      padding: 20px;
      position: relative;

      img {
        position: absolute;
        top: 0;
        right: 0;
        width: 30px;
      }
    }
    .first-open {
      background: #fff;
    }
  }
}
</style>
