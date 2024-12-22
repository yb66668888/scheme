<script setup>
import { ref } from 'vue'

const imgurl = ref('')


const getParams = () => {
  return {
    imgurl: imgurl.value
  }
}

defineExpose({ getParams })
</script>

<template>
    <div class="flex align-items-center flex-direction-column">
    <h3>最后一页：</h3>
    <el-input 
      v-model="imgurl" 
      class="width-230 margin-top-10" 
      placeholder="请输入图片链接"
      type="textarea"
      :autosize="{ minRows: 4, maxRows: 8 }"
      resize="none"
    />
  </div>
</template>