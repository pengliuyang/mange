<template>
  <div class="photocontent">
        <div class="top">
        <span class="title"><i class="el-icon-tickets"></i>图文样式内容编辑</span>
        <div>
          <a href="#/home/contentmange">&lt;&emsp;返回</a>
      </div>
    </div>
    <div class="contentbottom">
        <el-form :model="form">
            <el-form-item label="封面图" :label-width="formLabelWidth">
         <img id="preview" :src="imageUrl" width="250px" height="60px"/>
          <a href="javascript:;" class="file gradient">
          <input id="pop_file" type="file" accept=".jpg,.jpeg,.png" v-on:change="uploadFile($event)" name="fileTrans" ref="file" value="" />选择文件</a>
          </el-form-item>
              <el-form-item label="文章标题" :label-width="formLabelWidth">
            <el-input v-model="form.title" autocomplete="off"></el-input>
          </el-form-item>
                <el-form-item label="日期" :label-width="formLabelWidth">
            <el-col>
        <el-date-picker type="date" placeholder="选择日期" v-model="form.date1" style="width: 100%;"></el-date-picker>
        </el-col>
        </el-form-item>
               <el-form-item label="来源" :label-width="formLabelWidth">
            <el-input v-model="form.orignal" autocomplete="off"></el-input>
          </el-form-item>
              <el-form-item label="文章内容" :label-width="formLabelWidth">
       <!-- <quill-editor v-model="form.content" ref="myQuillEditor" style="height: 300px;" :options="editorOption">
      </quill-editor> -->
          </el-form-item>
   <el-button type="primary" round>主要按钮</el-button>
     <el-button type="info" round>信息按钮</el-button>
        </el-form>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
// import {
//     quillEditor
//   } from 'vue-quill-editor'
//   import 'quill/dist/quill.core.css'
//   import 'quill/dist/quill.snow.css'
//   import 'quill/dist/quill.bubble.css'
export default {
     components: {
      // quillEditor
    },
data(){
    return{
        imageUrl: '0.jpg',
        form: { title:"",date1:'',orignal:"",content: null, },
        formLabelWidth: "90px", 
        editorOption: {}
    }
}
,methods:{
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
        
addbanner: function() {
    var oFiles = document.getElementById("pop_file").files;
    var params = new FormData();
    params.append('file',oFiles[0]);
    axios({
        method: 'post',
        url: 'http://127.0.0.1:3000/product/upload',
        headers: {
            'Content-type': 'application/x-www-form-urlencoded;charset=UTf-8'
        },
        data: params
    })
    .then(function(response) {
        console.log(response);
    })
    
}
}
}
</script>

<style lang="less">
.photocontent{
    height: 100%;
    .top{
      display: flex;
      justify-content: space-between;
      border-bottom: 1px solid #ccc;
      height: 50px;
      line-height: 50px;
      a{
          text-decoration: none;
          color: skyblue;
      }
    }
    .contentbottom{
        margin-top: 20px;
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
    }
}
</style>