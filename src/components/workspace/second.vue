<script setup>
import { ref } from 'vue'

const content = ref('')

const getParams = () => {
  return {
    content: content.value
  }
}

defineExpose({ getParams })
</script>

<template>
    <div class="flex align-items-center flex-direction-column">
    <h3>第二页：</h3>
    <el-input 
      class="width-230 margin-top-10" 
      v-model="content" 
      placeholder="请输入内容" 
    />
  </div>
</template>