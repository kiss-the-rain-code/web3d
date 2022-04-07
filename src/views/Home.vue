<template>
  <el-container>
    <el-aside width="200px">菜单</el-aside>
    <el-container>
      <el-header>头部</el-header>
      <el-main>主体</el-main>
    </el-container>
  </el-container>
</template>

<script lang="ts">
import { Vue } from 'vue-class-component'

export default class Home extends Vue {

}
</script>

<style>
  .el-header {
    background-color: #B3C0D1;
    color: #333;
    text-align: center;
    line-height: 60px;
  }

  .el-aside {
    background-color: #D3DCE6;
    color: #333;
    text-align: center;
    line-height: 200px;
    height: 100%;
  }

  .el-main {
    background-color: #E9EEF3;
    color: #333;
    text-align: center;
    line-height: 160px;
  }

</style>
