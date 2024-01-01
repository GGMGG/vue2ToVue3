<template>
  <el-card class="box-card">
    <template #header>
      <div class="card-header">
        <span>Template中的Data变更</span>
      </div>
    </template>
    <div class="text item">
      转换后需为 Template 中的 Data 数据需加上 .data 前缀，其原因是许多开发者在Options API语法中做了改变引用类型数据地址的行为（如下），Data
      将会被转换为一个完整的对象以兼容此类操作，此方式额外产生的迭代成本更小
    </div>
    <div class="card-header">
      <span>Options API:</span>
    </div>
    <div class="text item">
      <vueCodeEdit v-model="descriptionsItem1" editorHeight="80" disabled="true" />
    </div>
    <div class="text item">
      <jsCodeEdit v-model="descriptionsItem2" editorHeight="260" disabled="true" />
    </div>
    <div class="card-header">
      <span>Composition API:</span>
    </div>
    <div class="text item">
      <vueCodeEdit v-model="descriptionsItem3" editorHeight="80" disabled="true" />
    </div>
    <div class="text item">
      <jsCodeEdit v-model="descriptionsItem4" editorHeight="80" disabled="true" />
    </div>
  </el-card>

  <el-card class="box-card">
    <template #header>
      <div class="card-header">
        <span>Vue2.7中延用Router3.x、Vuex3.x</span>
      </div>
    </template>
    <div class="text item">如若不想在 Vue2.7 项目中更新 Router4, Vuex4 ，可以从 Vue 实例中获取 Router, Route, Store</div>
    <div class="text item">
      <jsCodeEdit v-model="descriptionsItem5" editorHeight="150" disabled="true" />
    </div>
  </el-card>

  <el-card class="box-card">
    <template #header>
      <div class="card-header">
        <span>无法解析的内容</span>
      </div>
    </template>
    <div class="text item">动态变量或者拼接的内容无法被解析或解析错误</div>
    <div class="text item">
      <jsCodeEdit v-model="descriptionsItem6" editorHeight="200" disabled="true" />
    </div>
  </el-card>
</template>

<script setup lang="ts">
import jsCodeEdit from "@/components/jsCodeEdit/jsCodeEdit.vue";
import vueCodeEdit from "@/components/vueCodeEdit/vueCodeEdit.vue";

const descriptionsItem1 = `<template>
  <div>{{ userInfo }}</div>
</template>`;

const descriptionsItem2 = `export default {
  name: 'Sample',
  data() {
    return {
      userInfo: {}
    }
  },
  created() {
    this.userInfo = { name: 'Casey Adams', age: 80 }
  }
}`;

const descriptionsItem3 = `<template>
  <div>{{ toMarried(data.married) }}</div>
</template>`;

const descriptionsItem4 = `function toMarried(value) {
	return value ? 'Yes' : 'No'
}`;

const descriptionsItem5 = `import { getCurrentInstance } from 'vue'

const $vm = getCurrentInstance()
const router = $vm.proxy.$router
const route = $vm.proxy.$route
const store = $vm.proxy.$store`;

const descriptionsItem6 = `export default {
  methods: {
    onSubmit(propName) {
      this[propName] = '123'
      this.$emit(propName + '-change')
    }
  }
}`;
</script>

<style scoped>
.card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 5px;
  font-size: 20px;
}

.text {
  text-align: left;
  font-size: 16px;
}

.item {
  margin-bottom: 18px;
}

.box-card {
  margin-bottom: 18px;
}
</style>
