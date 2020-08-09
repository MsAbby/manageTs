<template>
  <div class="process-content">
    <div class="content" ref="content">
      <div
        id="myEcharts"
        ref="charts"
        style="width: 1000px; height: 800px"
      ></div>
    </div>
  </div>
</template>
<script lang="js">
import Vis from "vis";
// const echart = echarts as any;

export default {
  data() {
    return {
      nodes: [],
      edges: [],
      container: null,
      network: null,
      nodesArray:[
          {id: 0, label: '0', group: 0},
          {id: 1, label: "1", group: 0},
          {id: 2, label: "2", group: 0},
          {id: 3, label: "3", group: 1},
          {id: 4, label: "4", group: 1},
          {id: 5, label: "5", group: 1},
          {id: 6, label: "6", group: 2},
          {id: 7, label: "7", group: 2},
          {id: 8, label: "8", group: 2},
          {id: 9, label: "9", group: 3},
          {id: 10, label: "10", group: 3},
          {id: 11, label: "11", group: 3},
          {id: 12, label: "12", group: 4}
      ],
      edgesArray:[
          {from: 0, to: 1},
          {from: 0, to: 2},
          {from: 0, to: 3},
          {from: 1, to: 4},
          {from: 1, to: 5},
          {from: 1, to: 6},
          {from: 2, to: 7},
          {from: 2, to: 8},
          {from: 2, to: 9},
          {from: 3, to: 10},
          {from: 3, to: 11},
          {from: 3, to: 12},
      ],
      option: {
          autoResize: true,
          groups:{
              useDefaultGroups: true,
              myGroupId:{
              /*node options*/
              }
          },
          nodes: {
              shape: 'dot',
              size: 30,
              font: {
                  size: 32,
              },
              borderWidth: 2
          },
          edges: {
              width: 2,
              smooth:{  //设置两个节点之前的连线的状态
                  enabled: false  //默认是true，设置为false之后，两个节点之前的连线始终为直线，不会出现贝塞尔曲线
              }
          },
          physics: { //计算节点之前斥力，进行自动排列的属性
              enabled: true, //默认是true，设置为false后，节点将不会自动改变，拖动谁谁动。不影响其他的节点
              barnesHut: {
                  gravitationalConstant: -4000,
                  centralGravity: 0.3,
                  springLength: 120,
                  springConstant: 0.04,
                  damping: 0.09,
                  avoidOverlap: 0
              }
          },
          interaction:{
              dragNodes: true, //是否能拖动节点
              dragView: true, //是否能拖动画布
              hover: true, //鼠标移过后加粗该节点和连接线
              multiselect: true, //按 ctrl 多选
              selectable: true, //是否可以点击选择
              selectConnectedEdges: true, //选择节点后是否显示连接线
              hoverConnectedEdges: true, //鼠标滑动节点后是否显示连接线
              zoomView: true //是否能缩放画布
          },
          manipulation: {  //该属性表示可以编辑，出现编辑操作按钮
              enabled: true
          }
        }

    }
  },
  mounted() {
    this.init();
    // ÏÍ
},
  methods: {
    init() {
      // const _this = this;
      this.nodes = new Vis.DataSet(this.nodesArray);
      this.edges = new Vis.DataSet(this.edgesArray);
      this.container = document.getElementById('myEcharts');
      this.data = {
        nodes: this.nodes,
        edges: this.edges
      };
      this.network = new Vis.Network(this.container, this.data, this.option)
    }
  }
}
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
