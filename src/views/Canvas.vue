<template lang="pug">
  div#canvas
    input(
      type="button"
      value="add circle shape"
      @click="addShape"
    )
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
        )
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
  methods: {
    handleDragStart() {
      this.configText.text = 'dragging';
    },
    handleDragEnd() {
      this.configText.text = 'Some text here';
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
    }
  }
};
</script>
