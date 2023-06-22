<template>
  <div v-if="!mixinState.mSelectMode">
    <Divider plain orientation="left">Canvas {{ $t('size') }}</Divider>
    <Form :label-width="40">
      <FormItem :label="$t('width')" prop="name">
        <InputNumber
          disabled="true"
          :max="2000"
          :min="1"
          v-model="width"
          @on-change="setSize"
        ></InputNumber>
      </FormItem>
      <FormItem :label="$t('height')" prop="name">
        <InputNumber
          disabled="true"
          :max="2000"
          :min="1"
          v-model="height"
          @on-change="setSize"
        ></InputNumber>
      </FormItem>
    </Form>
    <Divider plain orientation="left">{{ $t('default_size') }}</Divider>
    <ButtonGroup vertical>
      <Button
        v-for="(item, i) in presetSize"
        :key="`${i}presetSize`"
        size="small"
        style="text-align: left"
        @click="setSizeBy(item.width, item.height)"
      >
        {{ item.label }}:{{ item.width }}x{{ item.height }}
      </Button>
    </ButtonGroup>
  </div>
</template>

<script setup name="CanvasSize">
import useSelect from '@/hooks/select';
import { useI18n } from 'vue-i18n';
import EditorWorkspace from '@/core/EditorWorkspace';

const { canvas, mixinState } = useSelect();
const { t } = useI18n();

let width = ref(1700);
let height = ref(760);
let presetSize = reactive([
  {
    label: t('default_floor_layout'),
    width: 1700,
    height: 760,
  },
]);

onMounted(() => {
  canvas.editor.editorWorkspace = new EditorWorkspace(canvas.c, {
    width: width.value,
    height: height.value,
  });
});

const setSizeBy = (w, h) => {
  width.value = w;
  height.value = h;
  setSize();
};
const setSize = () => {
  canvas.editor.editorWorkspace.setSize(width.value, height.value);
};
</script>

<style scoped lang="less">
:deep(.ivu-form-item) {
  margin-bottom: 0;
}
:deep(.ivu-divider-plain) {
  &.ivu-divider-with-text-left {
    margin: 10px 0;
    font-weight: bold;
  }
}
</style>
