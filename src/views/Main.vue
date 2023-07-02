<template>
  <div>
    <el-container>
      <el-aside width="auto">
        <Aside/>
      </el-aside>
      <el-container>
        <el-header>Header</el-header>
        <el-main>
          <router-view></router-view>
        </el-main>
      </el-container>
    </el-container>
  </div>
</template>

​<script>
import Aside from '../components/Aside.vue'
export default {
  data() {
    return {};
  },
  components: {
    Aside
  }
};
</script>