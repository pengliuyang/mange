<template>
  <div class="column">
    <div class="top">
      <span class="title"><i class="el-icon-s-home"></i>首页管理</span>
      <div>
        <el-button size="mini" type="primary" @click="fun()" v-show="!a"
          >编辑</el-button
        >
        <el-button size="mini" type="primary" @click="submit()" v-show="a"
          >保存</el-button
        >
        <el-button size="mini" type="primary" v-show="a">取消</el-button>
      </div>
    </div>
    <div class="contain">
      <div class="front" style="height:180px;width:100%">
        <el-image style="width: 100%; height:180px" :src="url"> </el-image>
        <div class="back" v-show="a" @click="changebanner()">
          <p>点击我更改banner</p>
        </div>
      </div>

      <div class="carousel front" >
        <div class="left front">
          <div class="input_video">
            <video-player
              class="video-player vjs-custom-skin"
              ref="videoPlayer"
              :playsinline="true"
              :options="playerOptions"
            ></video-player>
          </div>
        </div>
        <div class="right ">
          <h3>四川大学</h3>
          <p>
            四川大学大学巴适得板哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈嘻嘻嘻嘻嘻嘻嘻嘻嘻嘻呵呵呵呵呵呵哈哈哈红红火火恍恍惚惚红红火火恍恍惚惚红红火火恍恍惚惚哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊呵呵呵呵呵呵呵呵细细想想哦哦哦哦哦哦哦哦哦哦哦哦哦哦哦哦
          </p>
        </div>
          <div class="back" v-show="a"  @click="changecarousel()">
            <p>点击我更改视频图片文字描述</p>
          </div>
      </div>
      <div class="category">
        <h3 class="front">
          标题
          <div class="back" v-show="a">
            <p>点击我更改banner</p>
          </div>
        </h3>
        <div class="box1">
          <div class="front">
            <img src="3.jpg" alt="" />
            <p>虚拟仿真</p>
            <p>biubiu</p>
            <div class="back" v-show="a">
              <p>点击我更改banner</p>
            </div>
          </div>
          <div class="front">
            <img src="3.jpg" alt="" />
            <p>虚拟仿真</p>
            <p>biubiu</p>
            <div class="back" v-show="a">
              <p>点击我更改banner</p>
            </div>
          </div>
          <div class="front">
            <img src="3.jpg" alt="" />
            <p>虚拟仿真</p>
            <p>biubiu</p>
            <div class="back" v-show="a">
              <p>点击我更改banner</p>
            </div>
          </div>
        </div>
        <div class="box2">
          <div class="front">
            <img src="3.jpg" alt="" />
            <p>虚拟仿真</p>
            <p>biubiu</p>
            <div class="back" v-show="a">
              <p>点击我更改banner</p>
            </div>
          </div>
          <div class="front">
            <img src="3.jpg" alt="" />
            <p>虚拟仿真</p>
            <p>biubiu</p>
            <div class="back" v-show="a">
              <p>点击我更改banner</p>
            </div>
          </div>
          <div class="front">
            <img src="3.jpg" alt="" />
            <p>虚拟仿真</p>
            <p>biubiu</p>
            <div class="back" v-show="a">
              <p>点击我更改banner</p>
            </div>
          </div>
        </div>
      </div>
      <div class="article">
        <h3 class="front">
          标题
          <div class="back" v-show="a">
            <p>点击我更改banner</p>
          </div>
        </h3>
        <div class="articlelink">
          <h3 class="front">
            站内文章栏目链接
            <div class="back" v-show="a">
              <p>点击我更改banner</p>
            </div>
          </h3>
          <h3 class="front">
            站内文章栏目链接
            <div class="back" v-show="a">
              <p>点击我更改banner</p>
            </div>
          </h3>
        </div>
        <div class="articledetails">
          <img src="2.jpg" alt="" />
          <div>
            1
          </div>
        </div>
        <div class="articledetailsitem">
          <div>
            <img src="2.jpg" alt="" />
            <p>标题1</p>
            <p class="time">标题1</p>
          </div>
          <div>
            <img src="2.jpg" alt="" />
            <p>标题1</p>
            <p>标题1</p>
          </div>
          <div>
            <img src="2.jpg" alt="" />
            <p>标题1</p>
            <p>标题1</p>
          </div>
          <div>
            <img src="2.jpg" alt="" />
            <p>标题1</p>
            <p>标题1</p>
          </div>
        </div>
      </div>

      <div class="bottom front">
        666
        <div class="back" v-show="a">
          <p>点击我更改banner</p>
        </div>
      </div>
    </div>
    <div>
      <el-form
        :model="loginForm"
        :rules="rules"
        ref="loginFormId"
        label-width="80px"
        class="demo-ruleForm"
      >
        <el-form-item label="用户名">
          <el-input
            clearable
            type="text"
            v-model="loginForm.username"
            placeholder="用户名"
            autocomplete="off"
            prefix-icon="el-icon-s-custom"
          ></el-input>
        </el-form-item>
      </el-form>
    </div>
       <!-- 对话框
      <el-dialog title="添加栏目" :visible.sync="dialogFormVisible" width="50%">
     
        <div slot="footer" class="dialog-footer">
          <el-button @click="dialogFormVisible = false">取 消</el-button>
          <el-button type="primary" @click="dialogFormVisible = false">确 定</el-button>
        </div>
      </el-dialog> -->
  </div>
</template>

<script>
export default {
  data() {
    return {
         form: {
         name: "",
     
      },
      // dialogFormVisible: false,
      // formLabelWidth: "90px",
      a: false,
      changeCount: 0, // 判断表单数据是否改变过
      isPopup: false, // 判断提交事件不再弹出离开提示
      loginForm: {
        username: "",
      },
      url:
        "https://fuss10.elemecdn.com/1/34/19aa98b1fcb2781c4fba33d850549jpeg.jpeg",
      playerOptions: {
        playbackRates: [0.5, 1.0, 1.5, 2.0], //可选择的播放速度
        autoplay: false, //如果true,浏览器准备好时开始回放。
        muted: false, // 默认情况下将会消除任何音频。
        loop: false, // 视频一结束就重新开始。
        preload: "auto", // 建议浏览器在<video>加载元素后是否应该开始下载视频数据。auto浏览器选择最佳行为,立即开始加载视频（如果浏览器支持）
        language: "zh-CN",
        aspectRatio: "16:9", // 将播放器置于流畅模式，并在计算播放器的动态大小时使用该值。值应该代表一个比例 - 用冒号分隔的两个数字（例如"16:9"或"4:3"）
        fluid: true, // 当true时，Video.js player将拥有流体大小。换句话说，它将按比例缩放以适应其容器。
        sources: [
          {
            type: "",
            src: "1.mp4", //url地址
          },
        ],
        poster: "", //你的封面地址
        // width: document.documentElement.clientWidth,
        notSupportedMessage: "此视频暂无法播放，请稍后再试", //允许覆盖Video.js无法播放媒体源时显示的默认信息。
        controlBar: {
          timeDivider: true, //当前时间和持续时间的分隔符
          durationDisplay: true, //显示持续时间
          remainingTimeDisplay: false, //是否显示剩余时间功能
          fullscreenToggle: true, //全屏按钮
        },
      },
    };
  },
  methods: {
    fun() {
      this.a = true;
    },
    // 提交事件
    async submit() {
      this.isPopup = true;
    },
    changebanner(){
      alert(1)
    },
    changecarousel(){
      this.dialogFormVisible=true
    }
  },
  // 监听表单数据变化
  watch: {
    loginForm: {
      handler(val) {
        val && this.changeCount++;
      },
      deep: true,
    },
  },
  beforeRouteLeave(to, from, next) {
    if (this.changeCount && !this.isPopup) {
      // this.$confirm("数据尚未保存,确定要离开吗？")
      //   .then(() => {
      //     next();
      //   })
      //   .catch(() => {
      //     next(false);
      //   });    
       this.$confirm('你有内容正在编辑确定离开当前界面吗?', '提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'warning',
          center: true
        }).then(() => {
          next()
        }).catch(() => {
         next(false);
        })
    } else {
      next();
    }
  },
};
</script>
<style lang="less" scoped>
.column {
  height: 100%;
  .top {
    display: flex;
    justify-content: space-between;
    border-bottom: 1px solid #ccc;
    padding-bottom: 30px;
    .el-button {
      margin-top: 16px;
    }
    .el-icon-s-home {
      margin-right: 10px;
    }
  }
  .title {
    color: blue;
    margin-top: 18px;
     font-size: 20px;
  }
  i {
    font-size: 20px;
  }
  .contain {
    margin-top: 50px;
    .carousel {
      width: 100%;
      height: 316px;
      margin-top: 60px;
      display: flex;
      justify-content: space-between;

      .left {
        width: 57%;
        height: 316px;
      }
      .right {
        width: 400px;
        text-align: left;
        p {
          font-size: 18px;
          display: -webkit-box;
          overflow: hidden;
          white-space: normal !important;
          text-overflow: ellipsis;
          word-wrap: break-word;
          -webkit-line-clamp: 10;
          -webkit-box-orient: vertical;
          line-height: 24px;
        }
      }
    }
    .input_video .video-player {
      height: 100%;
    }
    .category {
      margin-top: 70px;

      img {
        width: 70px;
        height: 70px;
        border-radius: 35px;
      }
      h3 {
        width: 190px;
      }
    }
    .category > div {
      display: flex;
      justify-content: space-between;
      margin-top: 30px;
      div {
        width: 200px;
        height: 200px;
        text-align: center;
        transition: 1s;
        box-shadow: 1px 1px 4px #ccc;
      }
    }
    .box1 > div:hover {
      transform: scale(1.1);
    }
    .box2 > div:hover {
      transform: scale(1.1);
    }
    .article {
      margin-top: 70px;
      h3 {
        width: 190px;
      }
    }
    .articlelink {
      display: flex;
      justify-content: center;
      margin-top: 30px;
      margin-bottom: 40px;

      h3 {
        margin-right: 50px;
        font-size: 18px;
      }
    }
    .articledetails {
      display: flex;
      justify-content: space-between;
      img {
        width: 580px;
        height: 240px;
      }
      div {
        background: #e6e6e6;
        width: 400px;
      }
    }
    .articledetailsitem {
      display: flex;
      justify-content: space-between;
      margin-top: 20px;
      div {
        img {
          width: 180px;
        }
        p {
          font-size: 16px;
          color: #333;
          margin-top: 20px;
        }
        .time{
          margin-top: 10px;
        }
      }
    }
    .bottom {
      margin-top: 70px;
      background: #e6e6e6;
      height: 100px;
    }
    .front {
      position: relative;
      text-align: center;
    }
    .back {
      width: 100%;
      height: 100%;
      text-align: center;
      position: absolute;
      background: rgba(24, 22, 22, 0.7);
      top: 0;
      left: 0;
      font-size: 20px;
      color: white;
      display: flex;
      justify-content: center;
      align-items: center;
    }
  }
}
</style>
