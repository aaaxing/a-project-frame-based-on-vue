<template>
    <div class="layout"
    :style="{minHeight:windowInfo.height}"
    :class="bgImg"
    >
      <div class='left' :class="rightSide?'left-move':'left-stay'">
        <div class='sidebar' :class="leftSide?'left-show':'left-hide'">
            <Sidebar @fold='changeLeft' :status='leftSide'></Sidebar>
        </div>
        <div class='content'>
          <Header
            @fold="rightSide = !rightSide"
            @changeBg='changeBackground'
            :topShow = "topShow"
          ></Header>
          <Nav></Nav>
          <Content></Content>
          <Footer></Footer>
        </div>
      </div>
      <div class='right' :class="rightSide?'right-show':'right-hide'">
        456789
        dasfdasfdsfdasfdas
      </div>
    </div>
</template>
<script>
let limitWidth = 992 //限制左边菜单栏最小显示屏幕宽度
let topLimit = 1100  //顶部状态栏部分显示最小宽度
import Sidebar from "./Sidebar/index"
import Header from "./Header/index"
import Nav from './Nav/index'
import Footer from './Footer/index'
import Content from './Content/index'

export default {
  data () {
    //顶部菜单是否显示多余部分
    let topShow = false;
    //右边菜单的显示与隐藏
    let rightSide = false;
    //显示哪张背景图片
    let bgNumber = 1;
    //存储窗口信息
    let windowInfo = {
      width:"0px",
      height:"0px"
    };
    //左边菜单栏的展开与收缩
    let leftSide = true
    let leftLock = false
    let remberLeft = true
    let countLeft = 0;
    return {
      topShow,
      rightSide,
      windowInfo,
      bgNumber,
      leftSide,
      leftLock,
      remberLeft,
      countLeft
    }
  },
  created () {
    this.initWindowInfo()
  },
  components:{
    Sidebar,
    Header,
    Nav,
    Footer,
    Content
  },
  computed: {
    //背景图片
    bgImg(){
      return 'bg' + this.bgNumber
    }
  },
  methods: {
    //初始化页面高度,添加监听页面宽度,控制左侧菜单栏行为，监听页面宽度为limitWidth
    initWindowInfo(){
      this.windowInfo.width = window.innerWidth+"px"
      this.windowInfo.height = window.innerHeight+"px"
      if(window.innerWidth < limitWidth){
        this.leftLock = true
        this.leftSide = false
        this.countLeft = this.countLeft + 1
      }
      this.listenWidth(window.innerWidth)
      window.addEventListener('resize',(e) => {
        this.windowInfo.width = e.currentTarget.innerWidth+"px"
        this.windowInfo.height = e.currentTarget.innerHeight+"px"
        this.listenWidth(window.innerWidth)
        if(e.currentTarget.innerWidth < limitWidth){
          if(this.countLeft == 0){
            this.remberLeft = this.leftSide
          }
          this.leftSide = false;
          this.leftLock = true
          this.countLeft = this.countLeft + 1
        }else if(e.currentTarget.innerWidth > limitWidth){
          this.countLeft = 0
          this.leftSide = this.remberLeft
          this.leftLock = false
        }
      })
    },
    //根据宽度，判断顶部菜单显示状态
    listenWidth(width){
      if(width<=topLimit){
        this.topShow = false
      }else{
        this.topShow = true
      }
    },
    //换肤
    changeBackground(index){
      this.bgNumber = index
    },
    //左边菜单栏的展开与收缩
    changeLeft(){
      if(this.leftLock){
        return
      }
      this.leftSide = !this.leftSide
      this.remberLeft = this.leftSide
    }
  }
}
</script>
<style scoped>
    .layout{
      width:100%;
      position: relative;
    }
    .left{
      width:100%;
      background: rgba(255,255,255,0);
      position:relative;
      transition: all 0.3s ease;
      display: flex;
      align-items:flex-start;
    }
    .right{
      width:250px;
      background: rgba(255,255,255,0);
      position: absolute;
      top:0;
      transition: all 0.3s ease;
    }
    .right-show{
      right:0px;
    }
    .right-hide{
      right:-250px
    }
    .left-move{
      left:-250px
    }
    .left-stay{
      left:0;
    }
    .bg1{
      background: url("../../common/img/all/bg1.jpg") no-repeat 100% 100%;
      background-size:100% 100%;
    }
    .bg2{
      background: url("../../common/img/all/bg2.jpg") no-repeat 100% 100%;
      background-size:100% 100%;
    }
    .bg3{
      background: url("../../common/img/all/bg3.jpg") no-repeat 100% 100%;
      background-size:100% 100%;
    }
    .bg4{
      background: url("../../common/img/all/bg4.jpg") no-repeat 100% 100%;
      background-size:100% 100%;
    }
    .bg5{
      background: url("../../common/img/all/bg5.jpg") no-repeat 100% 100%;
      background-size:100% 100%;
    }
    .bg6{
      background: url("../../common/img/all/bg6.jpg") no-repeat 100% 100%;
      background-size:100% 100%;
    }
    .bg7{
      background: url("../../common/img/all/bg7.jpg") no-repeat 100% 100%;
      background-size:100% 100%;
    }
    .bg8{
      background: url("../../common/img/all/bg8.jpg") no-repeat 100% 100%;
      background-size:100% 100%;
    }
    .bg9{
      background: url("../../common/img/all/bg9.jpg") no-repeat 100% 100%;
      background-size:100% 100%;
    }
    .bg10{
      background: url("../../common/img/all/bg10.jpg") no-repeat 100% 100%;
      background-size:100% 100%;
    }
    .bg11{
      background: url("../../common/img/all/bg11.png") no-repeat 100% 100%;
      background-size:100% 100%;
    }
    .bg12{
      background: rgb(44, 62, 80);
      background-size:100% 100%;
    }
    .sidebar{
      width:250px;
      transition: all 0.3s ease;
      background: rgba(0 ,0,0,0);
    }
    .content{
      flex:1;
    }
    .left-show{
      width:250px;
    }
    .left-hide{
      width:50px
    }
</style>
