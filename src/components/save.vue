<!--
 * @Author: 秦少卫
 * @Date: 2022-09-03 19:16:55
 * @LastEditors: 秦少卫
 * @LastEditTime: 2023-05-07 09:34:18
 * @LastEditors: 秦少卫
 * @LastEditTime: 2023-04-10 14:33:18

 * @Description: 保存文件
-->

<template>
  <div class="save-box">
    <Button style="margin-left: 10px" type="text" @click="beforeClear">
      {{ $t('clear') }}
    </Button>
    <Button type="primary" @click="saveJson">
      {{ $t('keep') }}
    </Button>
    <!-- <Dropdown style="margin-left: 10px" @on-click="saveWith">
      <Button type="primary">
        {{ $t('keep') }}
        <Icon type="ios-arrow-down"></Icon>
      </Button>
      <template #list>
        <DropdownMenu>
          <DropdownItem name="clipboard">{{ $t('copy_to_clipboard') }}</DropdownItem>
          <DropdownItem name="saveImg">{{ $t('save_as_picture') }}</DropdownItem>
          <DropdownItem name="saveSvg">{{ $t('save_as_svg') }}</DropdownItem>
          <DropdownItem name="saveJson" divided>{{ $t('save_as_json') }}</DropdownItem>
        </DropdownMenu>
      </template>
    </Dropdown> -->
  </div>
</template>

<script setup name="save-bar">
import { Modal } from 'view-ui-plus';
import { clipboardText } from '@/utils/utils.ts';
import useSelect from '@/hooks/select';
import { v4 as uuid } from 'uuid';
import { debounce } from 'lodash-es';
import { useI18n } from 'vue-i18n';
const { t } = useI18n();

const apiUrl = import.meta.env.VITE_API_URL;

const { canvas } = useSelect();
const cbMap = {
  clipboard() {
    const jsonStr = canvas.editor.getJson();
    clipboardText(JSON.stringify(jsonStr, null, '\t'));
  },

  // async saveJson() {
  //   const dataUrl = canvas.editor.getJson();
  //   const fileStr = `data:text/json;charset=utf-8,${encodeURIComponent(
  //     JSON.stringify(dataUrl, null, '\t')
  //   )}`;
  //   downFile(fileStr, 'json');
  // },

  saveSvg() {
    // const workspace = canvas.c.getObjects().find((item) => item.id === 'workspace');
    // const { left, top, width, height } = workspace;
    // const dataUrl = canvas.c.toSVG({
    //   width,
    //   height,
    //   viewBox: {
    //     x: left,
    //     y: top,
    //     width,
    //     height,
    //   },
    // });
    // const fileStr = `data:image/svg+xml;charset=utf-8,${encodeURIComponent(dataUrl)}`;
    // downFile(fileStr, 'svg');
    // onCallback();
  },

  saveImg() {
    // const workspace = canvas.c.getObjects().find((item) => item.id === 'workspace');
    // canvas.editor.ruler.hideGuideline();
    // const { left, top, width, height } = workspace;
    // const option = {
    //   name: 'New Image',
    //   format: 'png',
    //   quality: 1,
    //   left,
    //   top,
    //   width,
    //   height,
    // };
    // canvas.c.setViewportTransform([1, 0, 0, 1, 0, 0]);
    // const dataUrl = canvas.c.toDataURL(option);
    // downFile(dataUrl, 'png');
    // canvas.editor.ruler.showGuideline();
    // onCallback();
  },
};

// const saveWith = debounce(function (type) {
//   cbMap[type] && typeof cbMap[type] === 'function' && cbMap[type]();
// }, 300);

/**
 * @desc clear canvas 清空画布
 */
const clear = () => {
  canvas.c.getObjects().forEach((obj) => {
    if (obj.id !== 'workspace') {
      canvas.c.remove(obj);
    }
  });
  canvas.c.discardActiveObject();
  canvas.c.renderAll();
};

async function saveJson() {
  const dataUrl = canvas.editor.getJson();
  // const fileStr = `data:text/json;charset=utf-8,${encodeURIComponent(
  //   JSON.stringify(dataUrl, null, '\t')
  // )}`;
  // downFile(fileStr, 'json');
  const params = typeof window !== 'undefined' ? window.localStorage.getItem('query_params') : null;
  if (params) {
    const { callbackUrl, floor_id } = JSON.parse(params);
    if (!floor_id) {
      return;
    }
    console.log({ apiUrl, params });
    await fetch(
      // apiUrl
      'http://localhost:8000/api' + '/rooms/draw/save',
      {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({
          floor_id,
          floor_drawing: dataUrl,
        }),
      }
    );
    onCallback(callbackUrl);
  }
}

const beforeClear = () => {
  Modal.confirm({
    title: t('tip'),
    content: `<p>${t('clearTip')}</p>`,
    okText: t('ok'),
    cancelText: t('cancel'),
    onOk: () => clear(),
  });
};

function onCallback(callbackUrl) {
  if (callbackUrl) {
    window.localStorage.removeItem('query_params');
    window.location.href = callbackUrl;
  }
}

function downFile(fileStr, fileType) {
  // const anchorEl = document.createElement('a');
  // anchorEl.href = fileStr;
  // anchorEl.download = `${uuid()}.${fileType}`;
  // document.body.appendChild(anchorEl); // required for firefox
  // anchorEl.click();
  // anchorEl.remove();
}
</script>
