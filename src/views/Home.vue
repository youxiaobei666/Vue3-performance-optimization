<template>
  <div
    class="container"
    v-loading="showLoading"
    element-loading-text="加载中..."
  >
    显示/隐藏<el-switch @change="showOrHiddenHandle" v-model="flag"></el-switch>

    <el-table class="table" :data="listData" border v-if="flag">
      <el-table-column label="姓名" width="180px">
        <template #default="scope">
          <el-icon><Avatar /></el-icon>
          <span> -{{ scope.row.name }}</span>
        </template>
      </el-table-column>
      <el-table-column v-for="item in listData" :key="item" width="80px">
        <template #default="scope">
          <el-icon><Star /></el-icon>
          <span>{{ scope.row.id }}</span>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue'
import { ElMessage } from 'element-plus'
// 是否转化的判断值
const flag = ref(true)
const showLoading = ref(false)

// 表格数据
const listData = shallowRef([])

// 假数据生成
let i = 1
while (i <= 100) {
  let id = i
  let name = 'name'
  let row = { id, name }
  listData.value.push(row)
  i++
}

const showOrHiddenHandle = (): void => {
  // 先展示 loading
  showLoading.value = true

  // 过 200ms 再控制显示
  setTimeout(() => {
    // 开始时间
    let startTime = +new Date()
    flag.value = true
    showLoading.value = false

    setTimeout(() => {
      // 结束
      let endTime = +new Date()

      ElMessage.success(`用时${(endTime - startTime) / 1000}s`)
    }, 0)
  }, 200)
}
</script>

<style lang="scss">
.container {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: start; // 列 从头开始排
  .table {
    margin-top: 20px;
    width: 80%;
  }
}
</style>
