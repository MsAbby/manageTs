<template>
  <div id="wrapper">
    <div class="line-wrap" style="margin-left: 70px;">
      <div id="item-1" class="state-item">State 1</div>
      <div id="item-2" class="state-item">State 2</div>
      <div id="item-3" class="state-item">State 3</div>
    </div>
    <div class="line-wrap">
      <div id="item-4" class="state-item">State 4</div>
      <div id="item-5" class="state-item">State 5</div>
      <div id="item-6" class="state-item">State 6</div>
      <div id="item-7" class="state-item">State 7</div>
    </div>
    <div class="line-wrap" style="margin-left: 215px;">
      <div id="item-8" class="state-item">State 8</div>
      <div id="item-9" class="state-item">State 9</div>
    </div>
  </div>
</template>
<script lang="ts">
import { Vue } from 'vue-property-decorator';
import jsPlumb from 'jsplumb';

const $jsPlumb = (jsPlumb.jsPlumb) as any;

export default class Process extends Vue {
    instance: any = null;

    init() {
        this.instance = $jsPlumb.getInstance({
            Container: 'workspace', //选择器id
            EndpointStyle: { radius: 0.11, fill: '#fff' }, // 端点样式
            // PaintStyle: { stroke: '#00ff00', strokeWidth: 2 }, // 绘画样式，默认8px线宽  #456
            // HoverPaintStyle: { stroke: '#1E90FF' }, // 默认悬停样式  默认为null
            // EndpointHoverStyle: { fill: '#F00', radius: 6 }, // 端点悬停样式
            // ConnectionOverlays: [ // 此处可以设置所有箭头的样式，因为我们要改变连接线的样式，故单独配置
            //   ['Arrow', { // 设置参数可以参考中文文档
            //     location: 1,
            //     length: 10,
            //     paintStyle: {
            //       stroke: '#496def',
            //       fill: '#496def'
            //     }
            //   }]
            // ],
            Connector: ['Straight', { gap: 1 }], // 要使用的默认连接器的类型：直线，折线，曲线等
            DrapOptions: { cursor: 'crosshair', zIndex: 2000 }
        });
        this.draw();
    }

    draw() {
        this.instance().connect({
          // 对应上述基本概念
          source: 'item-1',
          target: 'item-2',
          anchor: ['Left', 'Right', 'Top', 'Bottom', [0.3, 0, 0, -1], [0.7, 0, 0, -1], [0.3, 1, 0, 1], [0.7, 1, 0, 1]],
          connector: ['StateMachine'],
          endpoint: 'Blank',
          overlays: [ ['Arrow', { width: 8, length: 8, location: 1 }] ], // overlay
          // 添加样式
          paintStyle: { stroke: '#909399', strokeWidth: 2 }, // connector
          // endpointStyle: { fill: '#909399', outlineStroke: '#606266', outlineWidth: 1 } // endpoint
        })
    }
    mounted(){
        $jsPlumb.ready(() => {
            this.init();
        })
    }
}
</script>
<style scoped lang="scss">
     #wrapper {
    background:
      radial-gradient(
        ellipse at top left,
        rgba(255, 255, 255, 1) 40%,
        rgba(229, 229, 229, .9) 100%
      );
    height: 100vh;
    padding: 60px 80px;
    width: 100vw;
  }
  .state-item {
    width: 80px;
    height: 40px;
    color: #606266;
    background: #f6f6f6;
    border: 2px solid rgba(0, 0, 0, 0.05);
    text-align: center;
    line-height: 40px;
    font-family: sans-serif;
    border-radius: 4px;
    margin-right: 60px;
  }
  .line-wrap {
    display: flex;
  }
</style>
