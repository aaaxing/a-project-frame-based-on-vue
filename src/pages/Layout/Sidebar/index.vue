<template>
  <div class='side-container'>
    <div class='left-title animated fadeIn' v-show='status'>企业管理平台</div>
    <Icon type="navicon" @click.native="foldLeft" class='top-icon'></Icon>
    <div class='menu-box  animated fadeIn' v-show='status'>
      <div class='modal-box-l'>
        <div class='menu-title'>
          菜单列表
        </div>
        <Icon type="ios-cog" class='icon' style="float:right;margin-top:4px"></Icon>
        <ul>
          <li  v-for='(item,index) in menu' :key='index'>
            <span class='item-box' @click='openFirst(item)'>
              <Icon :type="item.icon" class='icon' style="float:left;line-height:45px;"></Icon>
              <span style="float:left">{{item.name}}</span>
              <img v-show='item.open' src='../../../common/img/other/minus.png' class='point'>
              <img v-show='!item.open' src='../../../common/img/other/plus.png' class='point'>
            </span>
            <ul class='ul' :style='item.open?`height:${item.child.length*45}px`:"height:0"'>
              <li v-for='(items,indexs) in item.child' :key='indexs' @click='clickMenu(items)'>
                <span class='item-box-s' :class='items.active?"item-box-s-c":""'>
                  <Icon :type="items.icon" class='icon' style="float:left;line-height:45px;"></Icon>
                  <span style="float:left">{{items.name}}</span>
                  <span class='number' :style="indexs%2==0?'background: #0DB8DF;':'background: #FF6B6B;'">{{indexs*3}}</span>
                </span>
              </li>
            </ul>
          </li>
        </ul>
      </div>
    </div>
    <div class='menu-box' v-show='!status' style='cursor:pointer'>
      <ul style='width:100%;'>
        <li v-for='(item,index) in menu' :key='index'>
          <Tooltip class='tooltips' :content="item.name" placement="right"  @click.native='openFirst(item)'>
            <Icon class='icon icon-sm' :type='item.icon'></Icon>
          </Tooltip>

          <ul class='ul' :style='item.open?`height:${item.child.length*40}px`:"height:0"'>
            <li v-for="(items,indexs) in item.child" :key='indexs'  @click='clickMenu(items)'>
              <Tooltip class='tooltipss' :content="items.name" placement="right" :class='items.active?"item-box-s-d":""'>
                <Icon class='icon icon-sm' :type='items.icon'></Icon>
              </Tooltip>
            </li>
          </ul>
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
export default {
  data () {
    let menu = [
      {
        name:"开发组功能",
        icon:"settings",
        open:false,
        child:[
          {name:"用户查询",icon:"person-stalker",active:false},
          {name:"功能维护",icon:"compass",active:false},
          {name:"企业用户管理",icon:"cube",active:false}
        ]
      },
      {
        name:"基础数据维护",
        open:false,
        icon:"link",
        child:[
          {name:"车辆信息管理",icon:"android-bus",active:false},
          {name:"从业人员管理",icon:"person-add",active:false},
          {name:"企业信息管理",icon:"ios-home",active:false},
          {name:"货物信息管理",icon:"ios-albums",active:false},
          {name:"客户人员管理",icon:"ios-pricetags",active:false},
          {name:"车队信息管理",icon:"android-list",active:false},
          {name:"统计单位维护",icon:"medkit",active:false},
          {name:"途径地管理",icon:"steam",active:false}
        ]
      },
      {
        name:"运单管理查询",
        open:false,
        icon:"document-text",
        child:[
          {name:"常规运单",icon:"android-document",active:false},
          {name:"计划运单",icon:"ios-paperplane",active:false},
          {name:"运单轨迹查询",icon:"android-map",active:false},
          {name:"车辆状态管理",icon:"android-options",active:false},
          {name:"品名信息查询",icon:"android-color-palette",active:false}
        ]
      },
      {
        name:"统计分析",
        open:false,
        icon:"stats-bars",
        child:[
          {name:"人员分类汇总",icon:"usb",active:false},
          {name:"车辆分类汇总",icon:"merge",active:false},
          {name:"货物运量统计",icon:"film-marker",active:false},
          {name:"货物流向统计",icon:"ios-timer",active:false},
          {name:"货物分类统计",icon:"ios-copy",active:false}
        ]
      },
      {
        name:"系统功能",
        icon:"key",
        open:false,
        child:[
          {name:"用户管理",icon:"ios-people",active:false},
          {name:"角色管理",icon:"man",active:false}
        ]
      }
    ]
    return {menu}
  },
  props:['fold','status'],
  methods: {
    //点击折叠左边菜单
    foldLeft(){
      this.$emit('fold')
    },
    //点击一级菜单
    openFirst(item){
      for(let i in this.menu){
        if(this.menu[i].name == item.name){
          this.menu[i].open = !this.menu[i].open
        }else{
          this.menu[i].open = false
        }
      }
    },
    //点击二级菜单，跳到相应页面
    clickMenu(item){
      for(let i in this.menu){
        for(let j in this.menu[i].child){
          if(this.menu[i].child[j].name == item.name){
            this.menu[i].child[j].active=true
          }else{
            this.menu[i].child[j].active=false
          }
        }
      }
    }
  }
}
</script>
<style scoped>
.side-container{
  position: relative;
  float: left;
  width:100%;
}
.left-title{
  margin-left:14px;
  font-size: 22px;
  line-height: 30px;
  font-weight: 200;
  width: 250px;
  letter-spacing: -1px;
  text-decoration: inherit;
  color: white;
  position: absolute;
  top:20px;
  transition: all 0.3s ease;
}
.menu-box{
  margin-top: 75px;
  width:100%;
}
.modal-box-l{
  margin:0px 10px;
  box-shadow: 0 1px 0 rgba(0, 0, 0, 0.3);
  background: rgba(0, 0, 0, 0.1);
  border-radius: 3px;
}
.menu-title{
  display: inline-block;
  background:rgba(0, 0, 0, 0.2);
  margin: 8px 0 8px 8px;
  border-radius: 20px;
  height: 22px;
  line-height: 20px;
  padding: 0 20px;
  color:white;
}
.item-box{
  cursor: pointer;
  text-align: left;
  position:relative;
  color:white;
  height:45px;
  line-height:45px;
  display:block;
  padding-left: 28px;
  box-sizing: border-box;
}
.item-box:hover{
  background-color: rgba(0, 0, 0, 0.2);
  color: white !important;
  border-left: 2px solid rgb(255, 255, 255);
}
.item-box:hover::after{
  width: 0px;
  height: 0px;
  position: absolute;
  top: 50%;
  margin-top: -3px;
  left: -6px;
  content: "";
  transform: rotate(90deg);
  border-bottom: 6px solid rgb(255, 255, 255);
  border-left: 8px solid transparent;
  border-right: 8px solid transparent;
}
.item-box-s{
  background: none 0px 0px repeat scroll rgba(0, 0, 0, 0.3);
  cursor: pointer;
  text-align: left;
  position:relative;
  color:white;
  height:45px;
  line-height:45px;
  display:block;
  padding-left: 40px;
  box-sizing: border-box;
}
.item-box-s:hover,.item-box-s-c{
  background-color: rgba(0, 0, 0, 0.2);
  color: white !important;
  border-left: 2px solid rgb(255, 255, 255);
}
.item-box-s:hover::after,.item-box-s-c::after{
  width: 0px;
  height: 0px;
  position: absolute;
  top: 50%;
  margin-top: -3px;
  left: -6px;
  content: "";
  transform: rotate(90deg);
  border-bottom: 6px solid rgb(255, 255, 255);
  border-left: 8px solid transparent;
  border-right: 8px solid transparent;
}
.ul{
  overflow: hidden;
  transition: height 0.5s ease;
}
.point{
  width: 15px;
  height: 15px;
  margin: 15px 20px 15px 0;
  float: right;
}
.number{
  color:#FFFFFF;
  border-radius: 3px;
  height: 20px;
  margin-top: 12.5px;
  line-height: 20px;
  float:right;
  margin-right: 20px;
  padding: 0 5px
}
</style>
<style>
.icon{
  color:white;
  font-size: 20px;
  width:30px;
  height: 30px;
  display: inline-block;
  line-height: 30px;
  vertical-align: center
}
.top-icon{
  color:rgba(255, 255, 255, 0.8);
  background: none repeat scroll 0 0 rgba(0, 0, 0, 0.3);
  width: 30px;
  height: 30px;
  text-align: center;
  border-radius: 3px;
  font-size:16px;
  line-height: 30px;
  cursor:pointer;
  position: absolute;
  right:10px;
  top:20px;
}
.top-icon:hover{
  background: none repeat scroll 0 0 rgba(0, 0, 0, 0.8);
}
.icon-sm{
  text-align: center;
  display: block;
  width:100%;
  font-size: 24px;
  height:40px;
  line-height: 40px;
}
.tooltips:hover,.tooltipss:hover,.icon-sm-s:hover,.item-box-s-d{
  background-color: rgba(0, 0, 0, 0.2) !important;
  text-shadow: none;
}
.tooltips,.tooltipss{
  text-align: center;
  width:50px;
  height: 40px;
}
.tooltipss{
  background: none repeat scroll 0 0 rgba(0, 0, 0, 0.3);
  color: rgba(255, 255, 255, 0.9) !important;
  outline: 0 none;
}
.tooltips .ivu-tooltip-inner,.tooltipss .ivu-tooltip-inner{
  height: 40px;
  border-radius: 0 6px 6px 0;
  background: #252D3B;
}
.tooltips .ivu-tooltip-popper[x-placement^=right] .ivu-tooltip-arrow,.tooltipss .ivu-tooltip-popper[x-placement^=right] .ivu-tooltip-arrow{
  border-right-color: #252D3B;
  border-width: 10px 10px 10px 0;
  margin-top:-10px;
  left:0px;
}
.tooltips .ivu-tooltip-popper,.tooltipss .ivu-tooltip-popper{
  z-index:10000;
  left:42px !important;
}
</style>
