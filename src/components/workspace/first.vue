<script setup>
import { ref } from 'vue'

const name = ref('')

const getParams = () => {
  return {
    name: name.value
  }
}

defineExpose({ getParams })

</script>

<template>
  <div class="flex align-items-center flex-direction-column">
    <h3>第一页：</h3>
    <el-input 
      class="width-230 margin-top-10" 
      v-model="name" 
      placeholder="请输入名称" 
    />
  </div>
</template>