
<template>
  <div class="column">
    <div class="top">
        <span class="title"><i :class="['el-icon-s-operation']
 "></i>栏目管理</span>
        <div>
         <!-- <span @click="returndata()">添加栏目</span> -->
         <el-button size="mini" @click="returndata()">添加栏目</el-button>
      </div>
    </div>
   <div class="addcolumn">
      <p>栏目列表</p>
     </div>
     <div class="mange">
<el-table
    :data="tableData"
    
    row-key="id"
    default-expand-all
    :tree-props="{children: 'children', hasChildren: 'hasChildren'}">
    <el-table-column
      prop="date"
      label="栏目"
      width="500">

    </el-table-column>
    <el-table-column
      align="center"
      label="显示"
      width="180">
        <template slot-scope="scope">
           <i class="el-icon-view" @click="handleDelete(scope.$index, scope.row)"></i>
   
      </template>
     
    </el-table-column>
    <el-table-column
      prop="address"
      label="操作"
       align="center">
    </el-table-column>
  </el-table>

     </div>
     <!-- 对话框 -->
      <el-dialog title="添加栏目" :visible.sync="dialogFormVisible" width="50%">
        <el-form :model="form">
          <el-form-item label="栏目名称" :label-width="formLabelWidth">
            <el-input v-model="form.name" autocomplete="off"></el-input>
          </el-form-item>
            <el-form-item label="栏目banner" :label-width="formLabelWidth">
         <img id="preview" :src="imageUrl" width="250px" height="60px"/>
          <a href="javascript:;" class="file gradient">
          <input id="pop_file" type="file" accept=".jpg,.jpeg,.png" v-on:change="uploadFile($event)" name="fileTrans" ref="file" value="" />选择文件</a>
          </el-form-item>
          <el-form-item label="展示类型" :label-width="formLabelWidth">
           <el-radio-group v-model="form.isPromotion">
              <el-radio label="图片列表">
                <img src="../../assets/images/btn_pic_1.png" alt="">
                <span>图片列表</span>
              </el-radio>
              <el-radio label="新闻列表">
                 <img src="../../assets/images/btn_pic_2.png" alt="">
                <span>新闻列表</span>

              </el-radio>
            </el-radio-group>
          </el-form-item>
         <el-form-item label="详情样式" :label-width="formLabelWidth">
           <el-radio-group v-model="form.isPromotion">
              <el-radio label="视频详情">
                  <img src="../../assets/images/btn_pic_3.png" alt="">
                  <span>视频详情</span>
              </el-radio>
              <el-radio label="富文本">
                  <img src="../../assets/images/btn_pic_4.png" alt="">
                  <span>富文本</span>
              </el-radio>
              <el-radio label="链接">
                 <img src="../../assets/images/icon_link.png" alt="">
                  <span>链接</span>
              </el-radio>
            </el-radio-group>
          </el-form-item>
          <el-form-item label="设置上级" :label-width="formLabelWidth">
          <div class="block">
 <el-cascader
    v-model="value"
    :options="options"
    @change="handleChange"></el-cascader>
</div>
          </el-form-item>
              <el-form-item label="打开方式" :label-width="formLabelWidth">
           <el-radio-group v-model="form.isPromotion">
              <el-radio label="当前窗口"></el-radio>
              <el-radio label="新窗口"></el-radio>
            </el-radio-group>
          </el-form-item>
        </el-form>
        <div slot="footer" class="dialog-footer">
          <el-button @click="dialogFormVisible = false">取 消</el-button>
          <el-button type="primary" @click="addbanner()">确 定</el-button>
        </div>
      </el-dialog>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  
  data(){
       return {
  options: [
         {
          value: 'ziyuan',
          label: '资源',
          children: [{
            value: 'axure',
            label: 'Axure Components'
          }, {
            value: 'sketch',
            label: 'Sketch Templates'
          }, {
            value: 'jiaohu',
            label: '组件交互文档'
          }]
        },
          {
          value: 'zhinan',
          label: '指南',
          children: [{
            value: 'shejiyuanze',
            label: '设计原则',
            children: [{
              value: 'yizhi',
              label: '一致'
            }, {
              value: 'fankui',
              label: '反馈'
            }, {
              value: 'xiaolv',
              label: '效率'
            }, {
              value: 'kekong',
              label: '可控'
            }]
          }]
        }, {
          value: 'zujian',
          label: '组件',
          children: [{
            value: 'basic',
            label: 'Basic',
            children: [{
              value: 'layout',
              label: 'Layout 布局'
            }, {
              value: 'color',
              label: 'Color 色彩'
            }, {
              value: 'typography',
              label: 'Typography 字体'
            }, {
              value: 'icon',
              label: 'Icon 图标'
            }, {
              value: 'button',
              label: 'Button 按钮'
            }]
          }, {
            value: 'form',
            label: 'Form',
            children: [{
              value: 'radio',
              label: 'Radio 单选框'
            }, {
              value: 'checkbox',
              label: 'Checkbox 多选框'
            }, {
              value: 'input',
              label: 'Input 输入框'
            }, {
              value: 'input-number',
              label: 'InputNumber 计数器'
            }, {
              value: 'select',
              label: 'Select 选择器'
            }, {
              value: 'cascader',
              label: 'Cascader 级联选择器'
            }, {
              value: 'switch',
              label: 'Switch 开关'
            }, {
              value: 'slider',
              label: 'Slider 滑块'
            }, {
              value: 'time-picker',
              label: 'TimePicker 时间选择器'
            }, {
              value: 'date-picker',
              label: 'DatePicker 日期选择器'
            }, {
              value: 'datetime-picker',
              label: 'DateTimePicker 日期时间选择器'
            }, {
              value: 'upload',
              label: 'Upload 上传'
            }, {
              value: 'rate',
              label: 'Rate 评分'
            }, {
              value: 'form',
              label: 'Form 表单'
            }]
          }, ]
        }],       
  imageUrl: '0.jpg',
  tableData: [{
          id: 1,
          date: '首页管理',
          name: "",
          address: <div><i class="el-icon-edit-outline" ></i><i class="el-icon-plus"></i><i class="el-icon-delete"></i></div> 
        }, 
         {
          id: 3,
          date: ' 项目介绍',
          name: <i class="el-icon-view"></i>,
          address: <div><i class="el-icon-edit-outline"></i><i class="el-icon-plus"></i><i class="el-icon-delete"></i></div> ,
          children: [{
              id: 31,
              date: '项目1',
              name:  <i class="el-icon-view"></i>,
              address: <div><i class="el-icon-edit-outline"></i><i class="el-icon-plus"></i><i class="el-icon-delete"></i></div> 
            }, {
              id: 32,
              date: '项目1-1',
              name: <i class="el-icon-view"></i>,
              address: <div><i class="el-icon-edit-outline"></i><i class="el-icon-plus"></i><i class="el-icon-delete"></i></div> 
          }]
        }
        ,
        {
          id: 2,
          date: '产品',
          name: <i class="el-icon-view"></i>,
          address: <div><i class="el-icon-edit-outline"></i><i class="el-icon-plus"></i><i class="el-icon-delete"></i></div> ,
           children: [{
              id: 21,
              date: '介绍',
              name:  <i class="el-icon-view"></i>,
              address: <div><i class="el-icon-edit-outline"></i><i class="el-icon-plus"></i><i class="el-icon-delete"></i></div> ,
                   children: [{
              id: 211,
              date: '项目1',
              name:  <i class="el-icon-view"></i>,
              address: <div><i class="el-icon-edit-outline"></i><i class="el-icon-plus"></i><i class="el-icon-delete"></i></div> 
            }, {
              id: 212,
              date: '项目1-1',
              name: <i class="el-icon-view"></i>,
              address: <div><i class="el-icon-edit-outline"></i><i class="el-icon-plus"></i><i class="el-icon-delete"></i></div>  
          }]

            }, {
              id: 22,
              date: '咨询',
              name: <i class="el-icon-view"></i>,
              address: <div><i class="el-icon-edit-outline"></i><i class="el-icon-plus"></i><i class="el-icon-delete"></i></div> 
          }]
        }],
        value: [],  
        form: {
        code: "",
        name: "",
        theclass: "",
        price: "",
        isPromotion: "",
        number: ""
      },
      dialogFormVisible: false,
      formLabelWidth: "90px"
    };
 },
    methods:{
        handleChange(value) {
        console.log(value);
      },
       handleDelete(index, row) {
        console.log(index, row);
      },
      
uploadFile:function(){
  
    const file = document.getElementById('pop_file');
    const fileObj = file.files[0];
    const windowURL = window.URL || window.webkitURL;
    // const img = document.getElementById('preview');
    if(file && fileObj) {
        const dataURl = windowURL.createObjectURL(fileObj);
       this.imageUrl=dataURl
        // img.setAttribute('src',dataURl);
    }
},
       returndata() {
      
      this.dialogFormVisible = true;  
    },

       load(tree, treeNode, resolve) {
        setTimeout(() => {
          resolve([
            {
              id: 31,
              date: '2016-05-01',
              name: '王小虎',
              address: '上海市普陀区金沙江路 1519 弄'
            }, {
              id: 32,
              date: '2016-05-01',
              name: '王小虎',
              address: '上海市普陀区金沙江路 1519 弄'
            }
          ])
        }, 1000)
      },
        
addbanner: function() {
    var oFiles = document.getElementById("pop_file").files;
    
    var params = new FormData();
    params.append('file',oFiles[0]);
    axios({
        method: 'post',
        url: 'http://127.0.0.1:3000/product/upload',
        // url: 'https://192.168.31.179:8081/article/articles',
        headers: {
            'Content-type': 'application/x-www-form-urlencoded;charset=UTf-8'
        },
        data: params
    }).then(function(response) {
        console.log(response);
    })
    

    
}
     
 },
 mounted(){
 }
}
</script>
<style lang="less">

.column{
    height: 100%;
    .top{
      display: flex;
      justify-content: space-between;
      border-bottom: 1px solid #ccc;
      padding-bottom: 30px;
      .el-button{
        margin-top: 16px;
      }
    }
    .title{
       color: blue;  
       margin-top: 18px; 
       font-size: 20px;
    }
    .addcolumn{
        margin-top: 20px;
        margin-bottom: 20px;
        font-size: 18px;
        color: #000;
    }
    i{
    font-size: 20px;
     margin-right: 10px;
    }
   .el-table{
       font-size: 16px;
       color: #333;
    
   }
  .file {
    position: relative;
    display: inline-block;
    background:skyblue;
    padding: 4px 20px;
    overflow: hidden;
    text-decoration: none;
    text-indent: 0;
    line-height: 20px;
    border-radius: 20px;
    color: #fff;
    font-size: 13px;
    margin-left: 18px;
}
.file input {
    position: absolute;
    font-size: 100px;
    left: 0;
    top: 0;
    opacity: 0;
}
.el-input__inner{
  width: 350px;
}
.el-dialog__header{
  text-align: center;
}
.el-dialog__header .el-dialog__title{
  border-bottom: 1px solid skyblue;  
  display: block;
  width: 80%;
  margin: 0 auto;
  padding: 0px 0px 10px 0px;
}
.dialog-footer{
display: flex;
  justify-content:center
}
   .el-table .has-gutter th div{
    font-size: 18px;
    color: #fff;
    background:#68b6c9;
    height: 40px;

   }
    .el-table td{
    // font-size: 16px;
    color: #333;
  }
  .el-table th>.cell{
   line-height: 40px;
   vertical-align: top;
  }

}


</style>