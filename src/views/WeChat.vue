<template>

  <div>

    <h3>微信公众号文章采集</h3>

    <el-table
        :data="tableData.list"
        border
        style="width: 100%"
        :cell-style="rowStyle"
    >
      <el-table-column
          prop="title"
          label="文章标题"
          align="center"
      >
      </el-table-column>


      <el-table-column
          label="文章链接"
          align="center"
      >
        <template v-slot="{ row }">
          <el-link type="success" :href="row.url" target="_blank">{{ row.title }}</el-link>
<!--          <a ></a>-->
        </template>
      </el-table-column>

      <el-table-column
          prop="publishTime"
          label="发布时间"
          align="center"
      >
      </el-table-column>

      <el-table-column
          prop="author"
          label="作者"
          align="center"
      >
      </el-table-column>

    </el-table>

    <div class="block" style="margin-top:15px;">
      <el-pagination
          @size-change="handleSizeChange"
          @current-change="handleCurrentChange"
          :current-page="currentPage"
          :page-sizes="[10, 15, 20, 25]"
          :page-size="pageSize"
          layout="total, prev, pager, next, jumper"
          :total="total">
      </el-pagination>
    </div>

  </div>

</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      tableData: {},
      // currentPage: 1, // 当前页码
      // total: 20, // 总条数
      // pageSize: 2 // 每页的数据条数
    }
  },
  mounted() {
    this.getLivestockInfo(1);  //因为刚加载显示第一页的数据，所以为1.
  },
  methods: {
    rowStyle() {
      return "text-align:center"
    },
    //每页条数改变时触发 选择一页显示多少行
    handleSizeChange(val) {
      console.log(`每页 ${val} 条`);
      this.currentPage = 1;
      this.pageSize = val;
    },
    //当前页改变时触发 跳转其他页
    handleCurrentChange(val) {
      console.log(`当前页: ${val}`);
      this.currentPage = val;
      this.getLivestockInfo(val);
    },
    getLivestockInfo(num1) {
      console.log(this)
      axios.get('http://127.0.0.1:5000/wx/wechat/getArticleList',
          {
            params: {
              start: num1
            }
          }
      ).then(resp => {
            this.tableData = resp.data.data;
            this.currentPage=num1;
            this.pageSize=this.tableData.pageSize;
            this.total=this.tableData.total;
          }



      ).catch(error => {  // 请求失败
        console.log('请求失败');
        console.log(error);
      })
    }
  }

}
</script>