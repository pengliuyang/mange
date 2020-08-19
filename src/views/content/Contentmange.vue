<template>
  <div class="content">
    <div class="top">
      <span class="title"><i class="el-icon-tickets"></i>内容管理</span>
      <div>
        <el-button size="mini" @click="returndata()">保存排序</el-button>
        <el-button size="mini" @click="addtitle()">新增文章</el-button>
        <el-button size="mini" @click="toggleSelection()">批量删除</el-button>
      </div>
    </div>
    <el-container>
      <el-aside width="200px">
        <el-menu
          default-active="2"
          unique-opened
          class="el-menu-vertical-demo"
          @open="handleOpen"
          @close="handleClose"
        >
          <el-menu-item index="3">
            <i class="el-icon-setting"></i>
            <span slot="title">首页内容</span>
          </el-menu-item>
          <el-submenu index="1">
            <template slot="title">
              <i class="el-icon-location"></i>
              <span>导航一</span>
            </template>
            <el-submenu index="1-4">
              <template slot="title"
                ><i class="el-icon-location"></i>选项4</template
              >
              <el-menu-item index="1-4-1"
                ><i class="el-icon-location"></i>选项1</el-menu-item
              >
            </el-submenu>
          </el-submenu>
          <el-submenu index="2">
            <template slot="title">
              <i class="el-icon-menu"></i>
              <span>导航二</span>
            </template>
            <el-submenu index="2-1">
              <template slot="title"
                ><i class="el-icon-location"></i>选项4</template
              >
              <el-menu-item index="2-1-1"
                ><i class="el-icon-document"></i>选项1</el-menu-item
              >
            </el-submenu>
          </el-submenu>
        </el-menu>
      </el-aside>
      <el-main>
        <el-table
          ref="multipleTable"
          :data="tableData"
          tooltip-effect="dark"
          style="width: 100%"
          @selection-change="handleSelectionChange"
          align='center'
        >
          <el-table-column type="selection" width="55" align='center'> </el-table-column>
          <el-table-column label="编号" width="60" align='center'>
            <template slot-scope="scope">{{ scope.row.index }}</template>
          </el-table-column>
          <el-table-column label="标题" width="120" align='center'>
            <template slot-scope="scope">{{ scope.row.title }}</template>
          </el-table-column>
          <el-table-column label="排序值" width="120" align='center'>
            <template slot-scope="scope">{{ scope.row.order }}</template>
          </el-table-column>
          <el-table-column label="日期" width="120" align='center'>
            <template slot-scope="scope">{{ scope.row.date }}</template>
          </el-table-column>
          <el-table-column label="状态" width="120" align='center'>
            <template slot-scope="scope"
              ><el-switch v-model="scope.row.value1"> </el-switch
            ></template>
          </el-table-column>
          <el-table-column label="操作" width="150" align='center'>
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
export default {
  data() {
    return {
      value1: true,
      tableData: [
        {
          index: 2,
          title: "四川大学",
          order: 2,
          date: "2016-05-03",
          value1: true,
        },
        {
          index: 2,
          title: "四川大学",
          order: 1,
          date: "2016-05-02",
          value1: true,
        },
        {
          index: 1,
          title: "四川大学",
          order: 1,
          date: "2016-05-04",
          value1: true,
        },
        {
          index: 1,
          title: "四川大学",
          order: 1,
          date: "2016-05-01",
          value1: true,
        },
        {
          index: 1,
          title: "四川大学",
          order: 1,
          date: "2016-05-08",
          value1: true,
        },
        {
          index: 1,
          title: "四川大学",
          order: 1,
          date: "2016-05-06",
          value1: true,
        },
        {
          index: 1,
          title: "四川大学",
          order: 1,
          date: "2016-05-07",
          value1: true,
        },
      ],
    };
  },
  methods: {
    toggleSelection(rows) {
      if (rows) {
        rows.forEach((row) => {
          this.$refs.multipleTable.toggleRowSelection(row);
        });
      } else {
        this.$refs.multipleTable.clearSelection();
      }
    },
    handleOpen(key, keyPath) {
      console.log(key, keyPath);
    },
    handleClose(key, keyPath) {
      console.log(key, keyPath);
    },
    handleSelectionChange(val) {
      this.multipleSelection = val;
    },
    handleEdit(index, row) {
      console.log(index, row);
      this.$router.push("/home/editphoto");
    },
    handleDelete(index, row) {
      console.log(index, row);
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
          this.$message({
            type: "success",
            message: "删除成功!",
            duration: 1000,
            onClose: () => {
              // axios.get(`http://127.0.0.1:3000/productbuy/del?id=${this.num}`).then(res=>{
              //     // console.log(res,row)
              //     if(res.data.success==true){
              //     }
              // })
            },
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
  },
};
</script>
<style lang="less" >
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
  i {
    font-size: 20px;
    margin-right: 10px;
  }
  .el-container {
    height: 90%;
    margin-top: 20px;
    // width: 800px;
    .el-main{
      margin-left: 0px;
      padding: 0px;
    }
   
    .el-aside {
      border-right: 1px solid #e6e6e6;
      .el-menu {
        border-right: 0px;
        .el-menu-item{
          font-size: 16px;
        }
        .el-submenu{
          .el-submenu__title{
        span{
          font-size: 16px;
        }
          }
        }
      }
    }
      .el-table td,.el-table .has-gutter th div{
         text-align: center;
  }
  //   .el-table .has-gutter th div{
  //   font-size: 18px;
  //   color: #fff;
  //   background:#68b6c9;
  //   height: 40px;
  //   line-height: 40px;
  //  }
  }
  .el-menu-item *{
    vertical-align: inherit;
  }
   .el-submenu__title *{
        vertical-align: inherit;
   }
     .el-table th>.cell{
   line-height: 40px;
   vertical-align: top;
  }
 
}
</style>
