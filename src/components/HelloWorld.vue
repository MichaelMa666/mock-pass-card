<template>
  <div class="hello">
    <div v-show="showPass">
      <h1>{{ msg }}</h1>
      <el-row type="flex" :gutter="20" justify="center">
        <el-date-picker
          v-model="dateSelected"
          type="date"
          placeholder="选择日期"
          format="yyyy 年 MM 月 dd 日"
          value-format="yyyy-MM-dd">
        </el-date-picker>
      </el-row>
      <el-row>
        <el-input placeholder="姓名" v-model="name"></el-input>
        <el-input placeholder="手机号" v-model="phoneNum"></el-input>
      </el-row>
      <el-row type="flex" :gutter="20" justify="center">
        <el-button type="danger" @click="generatePass()">生成出入证</el-button>
      </el-row>
    </div>
    <div v-show="!showPass">
      <div class="back-home" >
        <el-button class="bk-btn" @click="backHome()" size="small">退 出</el-button>
      </div>
      <div class="box">
        <div class="box-title">
          入楼凭证
          <img class="logo-img" src="../assets/logo1.png"/>
        </div>
        <div class="box-body">
          <div class="box-inner">
            <div class="box-info">
              <div class="box-info-icon"></div>
              <div class="box-info-detail">
                <div class="box-info-palace">泛利大厦</div>
                <div class="box-info-add">北京中关村融汇金融信息服务有限公司</div>
              </div>
            </div>
            <div class="box-info-name">{{ name }}</div>
            <div class="box-info-phone">{{ phoneNum.replace(/^(\d{3})\d{4}(\d+)/,"$1****$2") }}</div>
            <div class="box-time">{{ selectedTime }}</div>
            <div class="box-pass"></div>
          </div>
        </div>
        <div class="box-footer">
          <span></span>
          <span></span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data(){
    return {
      dateSelected:'',
      showPass: true,
      selectedTime:'',
      name: '马骁博',
      phoneNum: '13072096057'
    }
  },
  methods:{
    generatePass(){
      // console.log('this.dateSelected',this.dateSelected)
      if(this.dateSelected === ''){
        this.$message({
          message: '请选择日期',
          type: 'success'
        });
      }else{
        this.renderPass()
        this.showPass = !this.showPass
      }
      
    },
    backHome(){
      this.showPass = !this.showPass
    },
    renderPass(){
      // console.log('日期',this.dateSelected)
      var [,m,d] = this.dateSelected.split('-')
      this.selectedTime = m+'.'+d
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.el-row {
  margin-bottom: 20px;
}
@font-face{
    font-family: 'EurostileNextLTPro-SmBd';
    src : url('../assets/EurostileNextLTPro-SmBd.bb8ea922.otf');
}
@media screen and (min-width: 375px){
  .box{
    box-sizing: border-box;
      width: 351px;
      height: 508px;
      background-image: url('../assets/bg.png');
      background-size: cover;
      border-radius: 4px;
      margin: 24px auto auto;
  }
  .box-body{
    overflow: hidden;
    position: relative;
    box-sizing: border-box;
    margin: 0 auto;
    width: 311px;
    height: 400px;
    box-shadow: 0 1px 5px #000;
    border-radius: 5px;
    padding: 40px 0 0;
  }
  .box-title{
    height: 28px;
    font-size: 20px;
    font-family: PingFangSC-Semibold,PingFang SC;
    font-weight: 600;
    color: rgba(0,0,0,.85);
    line-height: 28px;
    padding: 24px 0 16px 16px;
    position: relative;
    text-align: left;
  }
  .logo-img{
    position: absolute;
    right: 16px;
    top: 10px;
    width: 191px;
    height: 48px;
  }
  .box-inner{
    padding: 0 20px;
  }
  .box-info{
    display: flex;
    flex-direction: row;
    align-items: center;
  }
  .box-info-icon{
    width: 40px;
    height: 40px;
    background-image: url('../assets/building.png');
    background-size: cover;
  }
  .box-info-detail{
    margin: 0 0 0 16px;
  }
  .box-info-palace{
    width: 216px;
    height: 33px;
    font-size: 24px;
    font-family: PingFangSC-Semibold,PingFang SC;
    font-weight: 600;
    color: #fff;
    line-height: 33px;
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 2;
  }
  .box-info-add{
    width: 216px;
    height: 17px;
    font-size: 12px;
    font-family: PingFangSC-Regular,PingFang SC;
    font-weight: 600;
    color: #fff;
    line-height: 17px;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    display: -webkit-box;
  }
  .box-info-name{
    min-height: 21px;
    font-size: 13px;
    font-family: PingFangSC-Medium,PingFang SC;
    font-weight: 600;
    color: #fff;
    line-height: 21px;
    margin: 14px 0 3px 56px;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    text-align: left;
  }
  .box-info-phone{
    width: 79px;
    height: 21px;
    font-size: 13px;
    font-family: PingFangSC-Regular,PingFang SC;
    font-weight: 600;
    color: #fff;
    line-height: 21px;
    margin-left: 56px;
  }
  .box-time{
    width: 89px;
    height: 36px;
    font-size: 35px;
    font-family: EurostileNextLTPro-SmBd;
    font-weight: 400;
    color: #fff;
    line-height: 43px;
    margin: 17px 0 23px 56px;
  }
  .box-pass{
    width: 139px;
    height: 139px;
    background-size: cover;
    background-image:url('../assets/pass.png');
  }
  .box-footer{
    margin-bottom: -20px;
  }
  .box-footer span{
    display: inline-block;
    width: 8px;
    height: 8px;
    margin: 0 3px;
    border-radius: 50%;
  }
  .box-footer span:nth-child(1){
    background: #888;
  }
  .box-footer span:nth-child(2){
    background: #ccc;
  }
}
.back-home{
  display: flex;
  align-items: center;
  justify-content: flex-end;
  width: 95vw;
  margin: 20px auto auto;
}
.bk-btn{
  font-size: 13px;
  line-height: 30px;
  color: #000;
  padding: 0 15px;
}
.box-body{
  background-image: url('../assets/building2.png');
}
</style>
