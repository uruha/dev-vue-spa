<template lang="pug">
  div#canvas
    div#options
      el-button(
        type="button"
        @click="addShape"
      ) add circl shape
    v-stage(:config="configKonva" ref="stage")
      v-layer(ref="layer")
        v-text(
          :config="configText"
          @dragstart="handleDragStart"
          @dragend="handleDragEnd"
        )
        v-circle(
          v-for="item in circleList"
          :key="item.id"
          :config="item"
          @dblclick="deleteShape(item)"
          @dragstart="handleDragStart"
          @dragend="handleDragEnd"
        )
    div#control
      el-button(
        type="button"
        @click="saveCanvas"
      ) save canvas
</template>

<script>
import Konva from 'konva';

const CANVAS_WIDTH = 600;
const CANVAS_HEIGHT = 400;

export default {
  data() {
    return {
      configKonva: {
        width: CANVAS_WIDTH,
        height: CANVAS_HEIGHT
      },
      configText: {
        text: 'Some text here',
        x: 50,
        y: 50,
        fontSize: 20,
        draggable: true,
        fill: 'black'
      },
      circleList: []
    };
  },
  created() {
    console.log(this);
  },
  mounted() {
    console.log(this.$el);
  },
  methods: {
    handleDragStart() {
      this.configText.text = 'dragging';
    },
    handleDragEnd(e) {
      this.configText.text = 'Some text here';

      // redraw moved shape postion
      const shape = e.target;
      const layer = this.$refs.layer.getNode();
      const stage = this.$refs.stage.getNode();
      shape.moveTo(layer);
      stage.draw();
    },
    addShape() {
      /** @sample access reference vue components */
      // const stage = this.$refs.stage.getStage();
      // const layers = stage.getLayers();
      // const layer = layers[0];

      const circleConfig = {
        x: Math.random() * 100,
        y: Math.random() * 100,
        radius: Math.random() * 100,
        fill: Konva.Util.getRandomColor(),
        stroke: 'black',
        strokeWidth: Math.random() * 10,
        draggable: true
      };

      this.circleList.push(circleConfig);
    },
    deleteShape(item) {
      console.log(item);
      console.log(this);
      // const deleteTarget = e.target;
      // deleteTarget.destroy();
      const target = this.circleList.indexOf(item);
      this.circleList.splice(target, 1);
    },
    saveCanvas() {
      console.log('save start...');
      const stage = this.$refs.stage.getStage();
      const jsonData = stage.toJSON();
      // const base64URL = stage.toDataURL();
      // const base64Data = base64URL.split(',');

      /** @sample konva の生成できるDATA */
      console.log(`stage data: ${jsonData}`);
      // console.log(`base64 URL: ${base64URL}`);
      // console.log(`base64 Data: ${base64Data[1]}`);

      /** @NOTE konva の生成するbase64はおそらく文字が多すぎてatobが使えない */
      // const decode = decodeURIComponent(escape(window.atob(base64URL)));
      // console.log(`decode base64: ${decode}`);
    }
  }
};
</script>
