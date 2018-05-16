<template>
  <div class='header-container'>
    <Poptip placement="bottom-start" class='poptips'>
      <div class='poptip-container'>
        <Icon class='nav-icon' type="chatbubble-working"></Icon>
        <div class='tag' style='background:#4AC4BC'>50</div>
      </div>
      <div slot='content'>
        <ul style="margin-bottom:0">
          <li v-for='(item,index) in message' :key="index" class='list top-nav-list'>
            <Icon type="chatbubble-working" class='list-icon'></Icon>
            <span class='item-name'>{{item.name}}</span>
            <span class='item-describe'>{{item.describe}}</span>
          </li>
        </ul>
        <div class='button'>查看所有公告</div>
      </div>
    </Poptip>
    <Poptip placement="bottom-start"  class='poptips'>
      <div class='poptip-container'>
        <Icon class='nav-icon' type="alert-circled"></Icon>
        <div class='tag' style='background:#EA3F3F'>50</div>
      </div>
      <div slot='content'>
        <ul style="margin-bottom:0">
          <li v-for='(item,index) in busremin' :key="index" class='list top-nav-list'>
            <Icon type="android-bus" class='list-icons'></Icon>
            <span class='item-name'>{{item.name}}</span>
            <span class='item-describe'>{{item.describe}}</span>
          </li>
        </ul>
        <div class='button'>进入列表</div>
      </div>
    </Poptip>
    <Poptip placement="bottom-start" class='poptips'>
      <div class='poptip-container'>
        <Icon class='nav-icon' type="help-buoy"></Icon>
        <div class='tag' style='background:#EA3F3F'>5</div>
      </div>
      <div slot='content'>
        <ul style="margin-bottom:0">
          <li v-for='(item,index) in person' :key="index" class='list top-nav-list'>
            <Icon type="person" class='list-icon'></Icon>
            <span class='item-name'>{{item.name}}</span>
            <span class='item-describe'>{{item.describe}}</span>
          </li>
        </ul>
        <div class='button'>进入列表</div>
      </div>
    </Poptip>

    <div class='time' v-show='topShow'>
      <div style="border-right: 1px solid rgba(0, 0, 0, 0.4);box-shadow: 1px 0 0 rgba(255, 255, 255, 0.1);">
        <Icon type="android-calendar" class='time-icon'></Icon>
        {{dateInfo.date}}
      </div>
      <div>
        <Icon type="android-time" class='time-icon'></Icon>
        {{dateInfo.time}}
      </div>
    </div>

    <Icon type="cube" class='list-icon top-right-fold-icon' @click.native='$emit("fold")'></Icon>

    <Poptip placement="bottom-end"  class='poptips' style="float:right;margin-right:30px;" v-show='topShow' v-model='poptips.bg'>
      <div class='poptip-container' style="margin-top:-2px">
        <Icon class='nav-icon' type="ios-keypad" style="float:left"></Icon>
        <span style="line-height:52px;float:left;color:white;margin-left:5px;">换肤</span>
      </div>
      <div slot='content'>
        <ul class='bg-container'>
          <li><img @click='changebg(1)' src="../../../common/img/all/s-bg-1.jpg"></li>
          <li><img @click='changebg(2)' src="../../../common/img/all/s-bg-2.jpg"></li>
          <li><img @click='changebg(3)' src="../../../common/img/all/s-bg-3.jpg"></li>
          <li><img @click='changebg(4)' src="../../../common/img/all/s-bg-4.jpg"></li>
          <li><img @click='changebg(5)' src="../../../common/img/all/s-bg-5.jpg"></li>
          <li><img @click='changebg(6)' src="../../../common/img/all/s-bg-6.jpg"></li>
          <li><img @click='changebg(7)' src="../../../common/img/all/s-bg-7.jpg"></li>
          <li><img @click='changebg(8)' src="../../../common/img/all/s-bg-8.jpg"></li>
          <li><img @click='changebg(9)' src="../../../common/img/all/s-bg-9.jpg"></li>
          <li><img @click='changebg(10)' src="../../../common/img/all/s-bg-10.jpg"></li>
          <li><img @click='changebg(11)' src="../../../common/img/all/s-bg-11.png"></li>
          <li><span @click='changebg(12)' style='background: rgb(44, 62, 80)'></span></li>
        </ul>
      </div>
    </Poptip>

    <Poptip placement="bottom-end"  class='poptips' style="float:right;margin-right:30px;">
      <span class='avtarss'>
        <img src="https://i.loli.net/2017/08/21/599a521472424.jpg"/>
      </span>
      <span style='color:white;margin-left:10px;cursor:pointer;line-height:45px;'>admin(超级管理员)▾</span>
      <div slot='content'>
        <span class='me'><Icon type="person" class='me-icon'></Icon>我的信息</span>
        <span class='me' style="border-bottom:1px solid #E5E5E5"><Icon type="ios-eye" class='me-icon'></Icon>修改密码</span>
        <span class='me'><Icon type="reply" class='me-icon'></Icon>退出登录</span>
      </div>
    </Poptip>
  </div>
</template>
<script>
const weekFormat = ["星期天","星期一","星期二","星期三","星期四","星期五","星期六"]
export default{
  data(){
    let dateInfo = {
      date:"",
      time:""
    }
    let poptips = {
      bg:false
    }
    let message = [
      {
        name:"公告1",
        describe:"2018-01-03"
      },
      {
        name:"公告2222",
        describe:"2018-04-09"
      },
      {
        name:"公告3333",
        describe:"2018-02-07"
      },
      {
        name:"公告44",
        describe:"2018-01-08"
      },
      {
        name:"公告555",
        describe:"2018-01-11"
      }
    ]
    let busremin = [
      {
        name:"云A1457挂 安全阈值检测有效期",
        describe:"2018-01-03"
      },
      {
        name:"云A1457挂 罐体检测有效期",
        describe:"2018-04-09"
      },
      {
        name:"云A1457挂 压力表检测有效期",
        describe:"2018-02-07"
      },
      {
        name:"云A1457挂 承运人责任险有效期",
        describe:"2018-01-08"
      },
      {
        name:"云A1457挂 罐体检测有效期",
        describe:"2018-01-11"
      }
    ]
    let person = [
      {
        name:"毕恩俊 诚信考核有效期",
        describe:"2018-01-03"
      },
      {
        name:"毕云毕 诚信考核有效期",
        describe:"2018-04-09"
      },
      {
        name:"陈关祥 诚信考核有效期",
        describe:"2018-02-07"
      },
      {
        name:"陈昆 诚信考核有效期",
        describe:"2018-01-08"
      },
      {
        name:"丁恒彦 诚信考核有效期",
        describe:"2018-01-11"
      }
    ]
    return {
      poptips,
      dateInfo,
      message,
      busremin,
      person
    }
  },
  props:['changeBg','fold',"topShow"],
  mounted(){
    //初始化时间
    this.initTime()
    setInterval(()=>{
      this.initTime()
    },1000)
  },
  methods:{
    //计算当前时间
    initTime(){
      let dateNow = new Date()
      let year = dateNow.getFullYear()
      let month = dateNow.getMonth()+1
      month = month<10?"0"+month:month
      let day = dateNow.getDate()
      day = day<10?"0"+day:day
      let week = dateNow.getDay()
      week = weekFormat[week]
      let hour = dateNow.getHours()
      hour = hour<10?"0"+hour:hour
      let minute = dateNow.getMinutes()
      minute = minute<10?"0"+minute:minute
      let second = dateNow.getSeconds()
      second = second<10?"0"+second:second
      let noon = hour>12?"下午":"上午"
      this.dateInfo.date = `${year}-${month}-${day}(${week})`
      this.dateInfo.time = `${noon}  ${hour} : ${minute} : ${second}`
    },
    //换肤
    changebg(index){
      this.poptips.bg = false
      this.$emit('changeBg',index)
    }
  }
}
</script>
<style scoped>
.header-container{
  width:100%;
  height: 65px;
  margin-top: 10px;
}
.poptip-container{
  cursor: pointer;
  height: 100%;
  padding: 0 12.5px;
  text-align: center;
  position: relative;
  display: inline-block;
}
.tag{
  position: absolute;
  width: 20px;
  height: 20px;
  line-height: 20px;
  color: white;
  font-size: 5px;
  right: 3px;
  top: 5px;
  border-radius: 100px;
}
.content-box{
  cursor: pointer;
}
.list{
  border-bottom: 1px solid #E5E5E5;
  height: 50px;
}
.list .item-name{
  cursor: pointer;
  line-height: 50px;
  margin-left: 15px;
  margin-right: 25px;
}
.list .item-describe{
  cursor: pointer;
  margin: 12.5px 10px 12.5px;
  display: inline-block;
  float:right;
  height: 25px;
  line-height: 25px;
  padding: 0 10px;
  border-radius:4px;
  background: #A8BDCF;
  color:white;
}
.button{
  width:100%;
  text-align: center;
  background:#A8BDCF ;
  cursor:pointer;
  height: 30px;
  line-height: 30px;
  margin: 10px 0;
  color: white
}
.button:hover{
  background: #0DB8DF
}
.avtarss{
  display: inline-block;
  width:45px;
  height:45px;
  cursor: pointer;
  border-radius: 100px;
}
.avtarss img{
  width: 100%;
  height: 100%;
  border-radius: 100px;
}
.me{
  display: block;
  cursor: pointer;
  color:#777777;
  line-height: 30px;
}
.time{
  display:inline-block;
  height:40px;
  background: none repeat scroll 0 0 rgba(0, 0, 0, 0.2);
  border: 1px solid rgba(0, 0, 0, 0.2);
  box-shadow: 0 1px 0 rgba(255, 255, 255, 0.1);
  color: #FFFFFF;
  float:left;
  margin:5px 0 0 20px;
  width: 330px;
  border-radius: 30px;
}
.time div{
  width:50%;
  box-sizing: border-box;
  display: inline-block;
  float: left;
  height: 20px;
  margin-top: 10px;
  text-align: center;
}
.time div .time-icon{
  font-size:15px;
  margin-right:5px;
  line-height:20px;
  display:inline-block;
  position: relative;top:1px
}
.bg-container{
  width:165px;
}
.bg-container li{
  width: 27.5px;
  height:27.5px;
  float:left;
}
.bg-container li img,.bg-container li span{
  width: 18.5px;
  height:18.5px;
  margin-left: 4.5px;
  border-radius: 100px;
  display: block;
  cursor: pointer;
}
</style>
<style>
.nav-icon{
  color: rgb(245, 245, 245) !important;
  font-size: 22px;
  line-height: 55px;
}
.poptips{
  float: left;
}
.poptips .ivu-poptip-title{
  display: none
}
.poptips .ivu-poptip-popper{
  top:67px !important;
  border-radius: 0;
}
.poptips .ivu-poptip-inner{
  border-radius: 0 0 4px 4px;
  box-shadow:0 0 0 white;
  border-right:1px solid #CCCCCC;
  border-left:1px solid #CCCCCC;
  border-bottom:1px solid #CCCCCC;
}
.poptips .ivu-poptip-arrow{
  border-width:0 10px 10px !important;
  top:-2px !important
}
.poptips .ivu-poptip-popper[x-placement^=bottom] .ivu-poptip-arrow{
  border-bottom-color:white !important;
}
.poptips .ivu-poptip-body{
  padding: 0
}
.list-icon{
  cursor: pointer;
  font-size: 25px;
  line-height: 50px;
  display: inline-block;
  float: left;
  margin-left:10px;
  color:#777777
}
.list-icons{
  cursor: pointer;
  font-size: 20px;
  display: inline-block;
  float: left;
  margin-left:10px;
  color:white;
  background:#DF2135;
  height:25px;
  width:24px;
  line-height:25px;
  text-align: center;
  border-radius: 100px;
  margin-top: 12.5px;
}
.top-nav-list:hover .list-icon,.top-nav-list:hover .item-name{
  color:#39B3D7;
}
.me .me-icon{
  font-size: 16px;
  display: inline-block;
  line-height: 30px;
  width: 20px;
  margin:0 0px 0 20px;
}
.me:hover{
  color:#39B3D7
}
.top-right-fold-icon{
  color:white;
  float:right;
  margin:-1px 30px 0 0;
  font-size:22px;
}
</style>
