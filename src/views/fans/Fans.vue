<template>
  <div>
    <el-card>
      <div slot="header">
        <el-breadcrumb separator-class="el-icon-arrow-right">
          <el-breadcrumb-item :to="{ path: '/home' }">首页</el-breadcrumb-item>
          <el-breadcrumb-item>粉丝设置</el-breadcrumb-item>
        </el-breadcrumb>
      </div>

      <el-tabs type="card" @tab-click="loadEcharts=true">
        <el-tab-pane label="粉丝列表"
          ><el-form v-loading="loading"><el-row :gutter="20">
            <el-col :span="4" v-for="(item, index) in fansList" :key="index"
              ><div class="fan-item">
                <img :src="item.url"></img>
                <span>{{item.id}}</span>
                <el-button type="primary" plain>+关注</el-button>
                </div
            ></el-col> </el-row
        ></el-form>
        <el-pagination
        layout="prev, pager, next"
        background
        :total="totalPages"
        :page-size="perPage"
        :current-page.sync="currentPage"
        @current-change="onCurrentChange"
        :disabled="loading"
      >
      </el-pagination>
      </el-tab-pane>

        <el-tab-pane label="粉丝画像">
          <template v-if="loadEcharts">
          <bar-chart></bar-chart>
        <baidu-map></baidu-map>
        </template></el-tab-pane>
      </el-tabs>

      
    </el-card>
  </div>
</template>

<script>
import { getFansList } from "@/api/user.js";

import { paginationMixin } from "@/utils/mixin";

import BaiduMap from "@/components/echarts/BaiduMap";
import BarChart from "@/components/echarts/BarChart.vue";

export default {
  name: "Fans",
  components: { BaiduMap, BarChart },
  props: {},
  mixins: [paginationMixin],
  data() {
    return {
      fansList: [],
      loadEcharts: false,
    };
  },
  computed: {},
  watch: {},
  created() {
    this.loadFansList();
  },
  mounted() {},
  methods: {},
};
</script>

<style lang='less' scoped>
.fan-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 150px;
  height: 200px;
  padding: 10px 0;
  margin-bottom: 20px;
  border: 1px dotted rgba(190, 131, 159, 0.5);
  img {
    width: 100px;
    height: 100px;
    border-radius: 50%;
  }
  span {
    margin: 20px 0;
  }
}
</style>
