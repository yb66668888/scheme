<script setup>
import { ref } from 'vue'

const type = ref('')
const enciphering = ref('')
const color = ref('')
const whileList = ref('')

const getParams = () => {
  return {
    type: type.value,
    enciphering: enciphering.value,
    color: color.value,
    whileList: whileList.value
  }
}

defineExpose({ getParams })
</script>

<template>
    <div class="flex align-items-center flex-direction-column">
    <h3>第三页：</h3>
    <el-select v-model="type" class="width-230 margin-top-10" placeholder="请选择字符串类型">
      <el-option label="字符串" value="string"></el-option>
      <el-option label="数字" value="number"></el-option>
      <el-option label="布尔值" value="boolean"></el-option>
      <el-option label="数组" value="array"></el-option>
      <el-option label="对象" value="object"></el-option>
    </el-select>

    <el-select v-model="enciphering" class="width-230 margin-top-10" placeholder="请选择是否显示加密">
      <el-option label="显示加密" value="1"></el-option>
      <el-option label="不显示加密" value="0"></el-option>
    </el-select>

    <el-select v-model="color" class="width-230 margin-top-10" placeholder="请选择颜色">
      <el-option label="红色" value="ref"></el-option>
      <el-option label="黑色" value="black"></el-option>
    </el-select>

    <el-input 
      v-model="whileList" 
      class="width-230 margin-top-10" 
      placeholder="请输入白名单"
      type="textarea"
      :autosize="{ minRows: 4, maxRows: 8 }"
      resize="none"
    />
  </div>
</template>