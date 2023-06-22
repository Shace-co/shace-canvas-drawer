<template>
  <Button type="text" @click="preview">
    {{ $t('preview') }}
  </Button>
</template>

<script lang="ts" setup>
import { fabric } from 'fabric';
import { ImagePreview } from 'view-ui-plus';
import vfe from 'vfe';

const canvas = inject('canvas') as vfe.ICanvas;
const getImgUrl = () => {
  canvas.editor.ruler.hideGuideline();
  const workspace = canvas.c.getObjects().find((item: fabric.Object) => item.id === 'workspace');
  const { left, top, width, height } = workspace as fabric.Object;
  const option = {
    name: 'New Image',
    format: 'png',
    quality: 1,
    width,
    height,
    left,
    top,
  };
  canvas.c.setViewportTransform([1, 0, 0, 1, 0, 0]);
  canvas.c.renderAll();
  const dataUrl = canvas.c.toDataURL(option);
  canvas.editor.editorWorkspace.auto();
  return dataUrl;
};
const preview = () => {
  const dataUrl = getImgUrl();
  ImagePreview.show({
    previewList: [dataUrl],
  });
};
</script>

<style scoped lang="less"></style>
