<!--
 * @Author: 秦少卫
 * @Date: 2022-09-03 19:16:55
 * @LastEditors: 秦少卫
 * @LastEditTime: 2023-02-25 21:53:19
 * @Description: 插入SVG元素
-->

<template>
  <div style="display: inline-block">
    <Dropdown transfer-class-name="fix" @on-click="insertTypeHand">
      <a href="javascript:void(0)">
        {{ $t('insertFile.insert') }}
        <Icon type="ios-arrow-down"></Icon>
      </a>
      <template #list>
        <DropdownMenu>
          <!-- 图片 image -->
          <DropdownItem name="insertImg">{{ $t('insertFile.insert_picture') }}</DropdownItem>
          <!-- SVG -->
          <DropdownItem name="insertSvg">{{ $t('insertFile.insert_SVG') }}</DropdownItem>
          <!-- SVG 字符串 string  -->
          <DropdownItem name="insertSvgStrModal">{{ $t('insertFile.insert_SVGStr') }}</DropdownItem>
        </DropdownMenu>
      </template>
    </Dropdown>
    <!-- 插入字符串svg元素 insert string svg -->
    <Modal
      v-model="showModal"
      :title="$t('insertFile.modal_tittle')"
      @on-ok="insertSvgStr"
      @on-cancel="showModal = false"
    >
      <Input
        v-model="svgStr"
        show-word-limit
        type="textarea"
        :placeholder="$t('insertFile.insert_SVGStr_placeholder')"
      />
    </Modal>
  </div>
</template>

<script>
import { compressImage, getImgStr, selectFiles } from '@/utils/utils';
import select from '@/mixins/select';
import { v4 as uuid } from 'uuid';

export default {
  name: 'ToolBar',
  mixins: [select],
  data() {
    return {
      showModal: false,
      svgStr: '',
    };
  },
  methods: {
    insertTypeHand(type) {
      this[type]();
    },
    // 插入图片 insert image
    insertImg() {
      selectFiles({ accept: 'image/*', multiple: true }).then((fileList) => {
        Array.from(fileList).forEach((file) => {
          compressImage(file, 0.5).then((compressedBase64) => {
            this.insertImgFile(compressedBase64);
          });
        });
      });
    },
    // 插入Svg insert svg
    insertSvg() {
      selectFiles({ accept: '.svg', multiple: true }).then((fileList) => {
        Array.from(fileList).forEach((item) => {
          getImgStr(item).then((file) => {
            this.insertSvgFile(file);
          });
        });
      });
    },
    // 插入SVG元素 insert svg element
    insertSvgStrModal() {
      this.svgStr = '';
      this.showModal = true;
    },
    // 插入图片文件 insert image file
    insertImgFile(file) {
      const imgEl = document.createElement('img');
      imgEl.src = file || this.imgFile;
      // 插入页面 insert page
      document.body.appendChild(imgEl);
      imgEl.onload = () => {
        // 创建图片对象 create image object
        const imgInstance = new this.fabric.Image(imgEl, {
          id: uuid(),
          name: '图片1',
          left: 100,
          top: 100,
        });
        // 设置缩放 set scale
        this.canvas.c.add(imgInstance);
        this.canvas.c.setActiveObject(imgInstance);
        this.canvas.c.renderAll();
        // 删除页面中的图片元素 delete image element in page
        imgEl.remove();
      };
    },
    // 插入文件元素 insert file element
    insertSvgFile(svgFile) {
      const This = this;
      this.fabric.loadSVGFromURL(svgFile || this.svgFile, (objects, options) => {
        const item = This.fabric.util.groupSVGElements(objects, {
          ...options,
          name: 'defaultSVG',
          id: uuid(),
        });
        This.canvas.c.add(item).centerObject(item).renderAll();
      });
    },
    // 插入字符串元素 insert string element
    insertSvgStr() {
      const This = this;
      this.fabric.loadSVGFromString(this.svgStr, (objects, options) => {
        const item = This.fabric.util.groupSVGElements(objects, {
          ...options,
          name: 'defaultSVG',
          id: uuid(),
        });
        This.canvas.c.add(item).centerObject(item).renderAll();
      });
    },
  },
};
</script>

<style scoped lang="less">
:deep(.ivu-select-dropdown) {
  z-index: 999;
}
</style>
