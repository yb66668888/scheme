<script setup>
import VueDraggableResizable from 'vue3-draggable-resizable'
import 'vue3-draggable-resizable/dist/Vue3DraggableResizable.css'
import html2canvas from 'html2canvas'
import { ElMessage } from 'element-plus'

import First from './components/workspace/first.vue'
import Second from './components/workspace/second.vue'
import Third from './components/workspace/third.vue'
import Fourth from './components/workspace/fourth.vue'
import Last from './components/workspace/last.vue'

import { ref, shallowRef } from 'vue'

// 侧边栏输入框
const asideInput = ref('') 
// 跳转页码
const num = ref(null) 
// 动态组件实例
const componentRef = ref(null) 
// 页码默认从1开始
const next = ref(1)

const components = [First, Second, Third, Fourth, Last]
const currentComponent = shallowRef(First)

const changeComponent = () => {
  // 创建前，获取当前页的参数
  const params = componentRef.value?.getParams()
  console.log('打印参数：', params)

  next.value ++
  if (next.value > components.length) {
    next.value = 1
  }

  currentComponent.value = components[next.value - 1]
}

// 输入页码跳转到下一页，并且下一页功能与"图片链接"页码互斥
const handleJump = (value) => {
  console.log(value)
  if (value > 5) {
    ElMessage.error('页码输入错误！')
    num.value = null
    return 
  }
  if (value === 5) {
    ElMessage.error('不可跳转到图片链接页面！')
    return 
  }
  
  next.value = value
  currentComponent.value = components[next.value - 1]
}

// 预览
const screenshot = ref(null)
const srcList = ref([])
const printPage = async () => {
  // window.print()
  try {
    const canvas = await html2canvas(document.body)
    screenshot.value = canvas.toDataURL('image/png')
    srcList.value.push(screenshot.value)
  } catch (error) {
    console.error('Error capturing screenshot:', error)
  }

}

</script>

<template>
  <div class="container">
    <div class="content">
      <div class="aside">
        <VueDraggableResizable 
          class="dragButton"
          :resizable="false"
          :w="90"
          :h="32"
          :x="105"
          :y="50"
          :parent="true"
        >
          <el-button type="primary">拖拽按钮</el-button>
        </VueDraggableResizable>
        
        <div class="aside-content">
          <div class="text-area">
            <div class="title">文本内容</div>
            <el-input class="width-230" v-model="asideInput" placeholder="请输入文本内容" />
          </div>

          <div class="img-area width-230">
            <el-image src="https://fuss10.elemecdn.com/e/5d/4a731a90594a4af544c0c25941171jpeg.jpeg" />
          </div>
        </div>
      </div>

      <div class="main">
        <div class="main-content">
          <component ref="componentRef" :is="currentComponent" />
        </div>

        <div class="next-page">
          <el-button type="primary" @click="changeComponent">下一页</el-button>
          <div class="jump">
            <span>跳转到</span>
            <el-input-number 
              v-model="num" 
              size="small" 
              :min="1"
              :controls="false" 
              @change="handleJump" 
            />
            <span>页</span>
          </div>
        </div>
      </div>
    </div>

    <!-- 预览页面 -->
    <el-dialog v-model="screenshot" title="预览" width="50%">
      <el-image :src="screenshot" :preview-src-list="srcList" />
    </el-dialog>
    
    <div class="footer">
      <el-button type="primary" @click="printPage">预览</el-button>
    </div>
  </div>
</template>

<style lang="less">
.container {
  width: 100vw;
  height: 100vh;
  background-color: #f5f5f5;
  .content {
    width: 100%;
    height: calc(100% - 50px);
    display: flex;
    .aside {
      width: 300px;
      border-right: 1px solid #ccc;
      position: relative;
      display: flex;
      flex-direction: column;
      align-items: center;
      .dragButton {
        z-index: 100;
      }
      .aside-content {
        margin-top: 110px;
        .text-area {
          .title {
            font-size: 14px;
            color: #333333;
            text-align: center;
            margin-bottom: 10px;
          }
        }
        .img-area {
          margin-top: 20px;
        }
      }
    }
    .main {
      flex: 1;
      position: relative;
      .main-content {
        width: 100%;
        height: 100%;
        background-color: #fff;
        padding: 50px;
      }
      .next-page {
        position: absolute;
        bottom: 20px;
        left: 50%;
        margin-left: -60px;
        display: flex;
        align-items: center;
        .jump {
          margin-left: 10px;
          color: #333333;
          font-size: 14px;
          display: flex;
          align-items: center;
          span {
            flex-shrink: 0;
          }
          .el-input-number {
            width: 40px;
            margin: 0 5px;
            input {
              text-align: center;
            }
          }
        }
        button {
          width: 120px;
        }
      }
    }
  }
  .preview {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
    img {
      max-width: 100%;
      max-height: 100%;
    }
  }
  .footer {
    height: 50px;
    border-top: 1px solid #ccc;
    display: flex;
    align-items: center;
    justify-content: center;
    button {
      width: 120px;
    }
  }
  .width-230 {
    width: 230px;
  }
  .vdr-container.active {
    border: none;
  }
}
</style>
