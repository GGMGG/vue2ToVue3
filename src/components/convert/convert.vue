<template>
  <el-row>
    <el-col :span="24">
      <div>
        <el-text class="mx-1" type="primary">{{ msg }}</el-text>
      </div>
    </el-col>
  </el-row>
  <el-row :gutter="20" :style="panelStyle">
    <el-col :span="11"><jsCodeEdit v-model="needToConvertStr" /></el-col>
    <el-col :span="2" :style="btnStyle"><el-button type="primary" @click="transition">转换</el-button></el-col>
    <el-col :span="11"><jsCodeEdit v-model="convertResult" /></el-col>
  </el-row>
  <descriptions></descriptions>
  <el-backtop :right="100" :bottom="100" />
</template>

<script setup lang="ts">
import { ref } from "vue";
import { ElNotification } from "element-plus";
import Vue2ToCompositionApi from "@/components/convert/convert.ts";
import jsCodeEdit from "@/components/jsCodeEdit/jsCodeEdit.vue";
import descriptions from "@/components/descriptions/descriptions.vue";

/**
 * props
 */
defineProps<{ msg: string }>();

/**
 * data
 */
const needToConvertStr = ref(`export default {
  name: 'Sample',
  props: {
    userInfo: {
      type: Object,
      required: false,
      default: () => ({
        userName: 'Todd Cochran',
        userAge: 20
      })
    }
  },
  data() {
    return {
      firstName: '',
      lastName: ''
    }
  }
}`);

const convertResult = ref("");

/**
 * method
 */
const transition = () => {
  let doConvertResult = { isSuccess: false, msg: "请输入需要转换的内容！" };
  if (needToConvertStr.value) {
    doConvertResult = Vue2ToCompositionApi(needToConvertStr.value);
    if (doConvertResult && doConvertResult.isSuccess) {
      convertResult.value = doConvertResult.msg;
    } else {
      showError(doConvertResult?.msg || "转换内容格式错误！");
    }
  } else {
    showError(doConvertResult?.msg || "转换内容不能为空！");
  }
};

const showError = (msg: string) => {
  ElNotification({
    title: "Error",
    message: msg,
    type: "error",
  });
};

/**
 * style
 */
const panelStyle = { marginTop: "50px" };
const btnStyle = { marginTop: "250px" };
</script>

<style scoped>
.el-row {
  margin-bottom: 20px;
}
.el-row:last-child {
  margin-bottom: 0;
}
.el-col {
  border-radius: 4px;
}
.grid-content {
  border-radius: 4px;
  min-height: 36px;
}
.el-text {
  font-size: 24px;
}
</style>
