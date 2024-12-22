<script setup>
import { ref } from 'vue'

const remark = ref('')
const bannerUrl = ref('')


const getParams = () => {
  return {
    remark: remark.value,
    bannerUrl: bannerUrl.value
  }
}

defineExpose({ getParams })
</script>

<template>
    <div class="flex align-items-center flex-direction-column">
    <h3>第四页：</h3>
    <el-input 
      v-model="remark" 
      class="width-230 margin-top-10" 
      placeholder="请输入说明"
      type="textarea"
      :autosize="{ minRows: 4, maxRows: 8 }"
      resize="none"
    />
    
    <el-input v-model="bannerUrl" class="width-230 margin-top-10" placeholder="请输入Banner链接"/>
    
  </div>
</template>