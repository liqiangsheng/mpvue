<template>
  <scroll-view class="meBox">
      <div class="header">
          <img :src="userInfo.avatarUrl" alt="" @click="loginClick">
          <!--<p open-type="getUserInfo" bindgetuserinfo="getUserInfo" >{{userInfo.name}}</p>-->
        <div>
          {{userInfo.nickName}}
          <button open-type="getUserInfo" @getuserinfo = 'bindgetuserinfo'> </button>
        </div>
      </div>
    <div>
       <p>{{addressObj.addressComponent.country}}-{{addressObj.addressComponent.province}}-{{addressObj.addressComponent.city}}-{{addressObj.addressComponent.district}}</p>
       <p> 详细地址：{{addressObj.formatted_address}}</p>
    </div>
  </scroll-view>
</template>

<script>

export default {
  components: {

  },

  data () {
    return {
        userInfo:{
          avatarUrl:'/static/images/defultphoto.png',
          nickName:'请登陆',
        },
      addressObj:{

      },
    }
  },
 methods:{

   bindgetuserinfo: function (e) {
     console.log(e)
    this.userInfo = e.mp.detail.userInfo
   }
 },
  created () {
    wx.getLocation({
      success:res=>{
        console.log(res,"he")
        wx.request({
          url:`https://restapi.amap.com/v3/geocode/regeo?key=df297249893d948553a71ea111d11384&location=${res.longitude},${res.latitude}&output=JSON`,
          success:res1=>{
            console.log(res1,"res1")
            this.addressObj = res1.data.regeocode
          }
        })
      }
    })
  }
}
</script>

<style scoped lang="less">
.meBox{
  width: 100%;
  background: #eee;
  .header{
    width: 100%;
    height: 280rpx;
    background: red;
    overflow: hidden;
    img{
       width: 120rpx;
       height: 120rpx;
       display: block;
       margin: 0 auto;
       margin-top: 40rpx;
     }
    div{
      width: 100%;
      text-align: center;
      line-height: 0.48rem;
      margin-top: 20rpx;
      font-size: 28rpx;
      font-weight: 900;
      position: relative;
      button{
        position: absolute;
        left: 0;
        top: 0;
        height: 100%;
        width: 100%;
        opacity: 0;
      }
    }
  }
}
</style>
