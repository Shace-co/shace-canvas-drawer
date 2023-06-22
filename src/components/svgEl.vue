<template>
  <div>
    <Divider plain orientation="left">{{ $t('eletronics') }}</Divider>
    <div class="box">
      <img
        v-lazy="`${repoSrc}svg/${item}.svg`"
        alt=""
        :key="item"
        v-for="item in getIndex(50, 75)"
        @click="addItem"
        :draggable="true"
        @dragend="dragItem"
      />
    </div>
    <Divider plain orientation="left">{{ $t('business') }}</Divider>
    <div class="box">
      <img
        v-lazy="`${repoSrc}svg/${item}.svg`"
        alt=""
        :key="item"
        v-for="item in getIndex(253, 261)"
        @click="addItem"
        :draggable="true"
        @dragend="dragItem"
      />
    </div>
  </div>
</template>

<script>
import { v4 as uuid } from 'uuid';
const defaultPosition = {
  left: 100,
  top: 100,
  shadow: '',
  fontFamily: '1-1',
};
export default {
  name: 'ToolBar',
  inject: ['canvas', 'fabric'],
  data() {
    return {
      repoSrc: import.meta.env.APP_REPO,
      arr: [],
    };
  },
  methods: {
    getIndex(start, end) {
      const arr = Array(end - (start - 1)).fill('');
      return arr.map((item, i) => i + start);
    },
    dragItem(event) {
      const url = event.target.src;
      // 会有性能开销 dragAddItem复用更简洁
      this.fabric.loadSVGFromURL(url, (objects) => {
        const item = this.fabric.util.groupSVGElements(objects, {
          shadow: '',
          fontFamily: 'arial',
          id: uuid(),
          name: 'svg元素',
        });
        this.canvas.editor.dragAddItem(event, item);
      });
    },
    // 按照类型渲染
    addItem(e) {
      const url = e.target.src;
      this.fabric.loadSVGFromURL(url, (objects, options) => {
        const item = this.fabric.util.groupSVGElements(objects, {
          ...options,
          ...defaultPosition,
          id: uuid(),
          name: 'svg元素',
        });
        this.canvas.c.add(item);
        this.canvas.c.setActiveObject(item);
        this.canvas.c.requestRenderAll();
      });
    },
  },
};
</script>

<style scoped lang="less">
img {
  display: inline-block;
  width: 53px;
  margin-left: 2px;
  margin-bottom: 2px;
  background: #f5f5f5;
  padding: 6px;
  cursor: pointer;
}
</style>
