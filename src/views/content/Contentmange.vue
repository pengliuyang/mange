<template>
  <div class="content">
    <div class="top">
      <span class="title"><i class="el-icon-tickets"></i>内容管理</span>
      <div>
        <el-button size="mini" @click="keepOrder()">保存排序</el-button>
        <el-button size="mini" @click="addtitle()">新增文章</el-button>
        <el-button size="mini" @click="toggleSelection()">批量删除</el-button>
      </div>
    </div>
    <el-container>
      <el-aside width="210px">
        <Child :dataList="listData"></Child>
      </el-aside>
      <el-main>
        <el-table
          ref="multipleTable"
          :data="tablelist"
          tooltip-effect="dark"
          style="width: 100%"
          @selection-change="handleSelectionChange"
          align="center"
        >
          <el-table-column type="selection" width="55" align="center">
          </el-table-column>
          <el-table-column label="编号" width="60" align="center">
            <template slot-scope="scope">{{ scope.row.id }}</template>
          </el-table-column>
          <el-table-column label="标题" width="120" align="center">
            <template slot-scope="scope">{{ scope.row.title }}</template>
          </el-table-column>
          <el-table-column label="排序值" width="100" align="center">
            <template slot-scope="scope">
              <el-input-number
                v-model="scope.row.sort"
                controls-position="right"
                :min="1"
                :max="10"
              ></el-input-number>
            </template>
          </el-table-column>
          <el-table-column label="日期" width="120" align="center">
            <template slot-scope="scope">{{ scope.row.createTime }}</template>
          </el-table-column>
          <el-table-column label="状态" width="120" align="center">
            <template slot-scope="scope"
              ><el-switch
                :active-value="0"
                :inactive-value="1"
                v-model="scope.row.isShow"
                @change="text(scope.row)"
              >
              </el-switch
            ></template>
          </el-table-column>
          <el-table-column label="操作" width="150" align="center">
            <template slot-scope="scope">
              <el-button
                size="mini"
                @click="handleEdit(scope.$index, scope.row)"
                >编辑</el-button
              >
              <el-button
                size="mini"
                type="danger"
                @click="
                  open();
                  handleDelete(scope.$index, scope.row);
                "
                >删除</el-button
              >
            </template>
          </el-table-column>
        </el-table>
      </el-main>
    </el-container>
  </div>
</template>

<script>
import Child from "@/components/Childmenu.vue";
import { allColumn } from "@/apis/request.js";
import { deleteArticle } from "@/apis/request.js";
import { editArticle } from "@/apis/request.js";
import { getColumnarticle } from "@/apis/request.js";
import moment from "moment";
export default {
  data() {
    return {
      deleteid: 0,
      value1: 0,
      listData: [
        {
          name: "钠管设备",
          id: "1",
          level: 1,
          child: [
            {
              name: "系统默认组",
              id: "2",
              flag: true,
            },
            {
              name: "设备一组",
              id: "3",
              child: [
                {
                  name: "一组A小组",
                  id: "4",
                  child: [
                    {
                      name: "一组A小组的成员1",
                      id: "5",
                    },
                    {
                      name: "一组A小组的成员2",
                      id: "6",
                      child: [
                        {
                          name: "一组A小组的成员何总",
                          id: "7",
                        },
                        {
                          name: "一组A小组的成员曾",
                          id: "8",
                        },
                        {
                          name: "一组A小组的成员飘总",
                          id: "9",
                        },
                      ],
                    },
                  ],
                },
                {
                  name: "一组B小组",
                  id: "10",
                },
              ],
            },
            {
              name: "设备二组",
              id: "11",
            },
          ],
        },
      ],

      multipleSelection: [],
    };
  },
  components: {
    Child,
  },

  methods: {
    toggleSelection() {
      this.open();
    },
    text(row) {
      this.$store.state.editid = row;
      var form = { ...this.$store.state.editid };
      var date = moment(form.createTime).format("YYYY-MM-DD");
      form.createTime = date;
      var arr = [];
      arr.push(form);

      editArticle(arr).then((res) => {
        console.log(res);
      });
    },
    handleSelectionChange(val) {
      this.deleteid = val.map((res) => {
        return res.id;
      });
      console.log(this.deleteid);
    },
    handleEdit(index, row) {
      console.log(index, row);
      this.$store.state.editid = row;
      this.$router.push("/home/editphoto");
    },
    handleDelete(index, row) {
      console.log(index, row);
      this.deleteid = row.id;
    },
    addtitle() {
      this.$router.push("/home/addtitle");
    },
    open() {
      // const a=this;
      this.$confirm("此操作将永久删除该栏目内容, 是否继续?", "提示", {
        confirmButtonText: "确定",
        cancelButtonText: "取消",
        type: "warning",
        center: true,
      })
        .then(() => {
          deleteArticle(this.deleteid).then((res) => {
            if (res == 1) {
              getColumnarticle(this.$store.state.columnid).then((res) => {
                this.$store.state.article = res;
              });
            }
          });
        })
        .catch(() => {
          this.$message({
            type: "info",
            message: "已取消删除",
            duration: 1000,
          });
        });
    },
    keepOrder() {
      console.log(this.tablelist);
      editArticle(this.tablelist).then((res) => {
        console.log(res);
      });
    },
  },
  computed: {
    tablelist() {
      if (this.$store.state.article.length != 0) {
        return this.$store.state.article;
      } else {
        return "";
      }
    },
  },
  mounted() {
    allColumn().then((res) => {
      this.listData = res;
      // console.log(res);
    });
  },
};
</script>
<style lang="less">
.content {
  height: 100%;
  .top {
    display: flex;
    justify-content: space-between;
    border-bottom: 1px solid #ccc;
    padding-bottom: 30px;
    .el-button {
      margin-top: 16px;
    }
  }
  .title {
    color: blue;
    margin-top: 18px;
    font-size: 20px;
  }
  .el-icon-tickets {
    font-size: 20px;
    margin-right: 10px;
  }
  .el-container {
    height: 90%;
    margin-top: 20px;
    // width: 800px;
    .el-main {
      margin-left: 0px;
      padding: 0px;
    }

    .el-aside {
      border-right: 1px solid #e6e6e6;
      .el-menu {
        border-right: 0px;
        .el-menu-item {
          font-size: 16px;
        }
        .el-submenu {
          .el-submenu__title {
            span {
              font-size: 16px;
            }
          }
        }
      }
    }
    .el-table td,
    .el-table .has-gutter th div {
      text-align: center;
    }
    .el-table .has-gutter th div {
      font-size: 18px;
      color: #fff;
      background: #68b6c9;
      height: 40px;
      line-height: 40px;
    }
  }
  .el-menu-item * {
    vertical-align: inherit;
  }
  .el-submenu__title * {
    vertical-align: inherit;
  }
  .el-table th > .cell {
    line-height: 40px;
    vertical-align: top;
  }
  .el-input {
    width: 100px;
  }
  .el-input-number {
    width: 100px;
  }
}
</style>
