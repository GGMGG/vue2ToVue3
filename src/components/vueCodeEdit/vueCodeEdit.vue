<template>
  <codemirror
    v-model="code"
    :placeholder="editorPlaceholder"
    :style="{ height: editorHeight + 'px', width: editorWidth + '%', textAlign: 'left', fontSize: editorFontSize + 'px' }"
    :autofocus="false"
    :disabled="false"
    :indent-with-tab="false"
    :tabSize="tabSize"
    :extensions="extensions"
    :scrollbarStyle="null"
  />
</template>

<script setup lang="ts">
import { ref, computed } from "vue";
import { Codemirror } from "vue-codemirror";
import { vue } from "@codemirror/lang-vue";
import { oneDark } from "@codemirror/theme-one-dark";

const emit = defineEmits();
const props = defineProps({
  value: {
    type: String,
    default: "",
  },
  editorPlaceholder: {
    type: String,
    default: "请输入代码",
  },
  editorHeight: {
    type: String,
    default: "500",
  },
  editorWidth: {
    type: String,
    default: "100",
  },
  editorFontSize: {
    type: String,
    default: "16",
  },
  tabSize: {
    type: Number,
    default: 4,
  },
});
const _value = computed({
  get() {
    return props.value || "";
  },
  set(value) {
    emit("update:value", value);
  },
});
const code = ref();
const extensions = [vue(), oneDark];
</script>
