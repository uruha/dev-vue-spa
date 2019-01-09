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
          @dblclick="deleteShape(item)"
          @dragstart="handleDragStart"
          @dragend="handleDragEnd"
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
    }
  }
};
</script>
