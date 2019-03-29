<template>
  <div @click="clickHandle">

    <div class="userinfo" >
       <div class="box">
         1111
       </div>
    </div>

    <div class="usermotto">
      <div class="user-motto">
        <card :text="motto"></card>
      </div>
    </div>

    <form class="form-container">
      <input type="text" class="form-control" :value="motto" placeholder="v-model" />
      <input type="text" class="form-control" v-model="motto" placeholder="v-model" />
      <input type="text" class="form-control" v-model.lazy="motto" placeholder="v-model.lazy" />
    </form>

    <a href="/pages/counter/main" class="counter">去往Vuex示例页面</a>

    <div class="all">
        <div class="left">
        </div>
        <div class="right">
        </div>
    </div>
  </div>
</template>

<script>
import card from '@/components/card'
import store from '../counter/store'
export default {
  data () {
    return {
      arrData:[
        {a:'1',b:"aa"},
        {a:'2',b:"bb"},
        {a:'3',b:"cc"},
        {a:'4',b:"dd"},
        {a:'4',b:"ee"},
        {a:'4',b:"ff"},
        {a:'4',b:"gg"},
      ],
      motto: 'Hello miniprograme',
      userInfo: {
        nickName: this.$name,
        avatarUrl: 'http://mpvue.com/assets/logo.png'
      }
    }
  },
  computed: {
    count () {
      return store.state.count
    }
  },
  components: {
    card
  },

  methods: {
    bindViewTap () {
      const url = '../logs/main'
      if (mpvuePlatform === 'wx') {
        mpvue.switchTab({ url })
      } else {
        mpvue.navigateTo({ url })
      }
    },
    increment () {
        store.commit('increment')
    },
    decrement () {
      store.commit('decrement')
    },
    clickHandle (ev) {
      console.log('clickHandle:', ev)
      // throw {message: 'custom test'}
    }
  },

  created () {
    let data=[];
    for (let i = 0; i < this.arrData.length; i++) {
      this.arrData[i].b = [this.arrData[i].b]
      let flag = false;
      for (let j = 0; j < data.length; j++) {
        if (data[j].a == this.arrData[i].a) {
          data[j].b  =  [...data[j].b,...this.arrData[i].b];
          flag = true;
           break;
        }
      }
      if (!flag) {
        data.push(this.arrData[i])
      }

    }
    console.log(data, 'data')
    wx.getSystemInfo({
      success(res) {
//        console.log(111111111111)
      }
    })
  }
}
</script>

<style scoped lang="less">
.userinfo {
  display: flex;
  flex-direction: column;
  align-items: center;
  .box{
    width: 100rpx;
    height: 50rpx;
    background: red;
  }
}

.userinfo-avatar {
  width: 128rpx;
  height: 128rpx;
  margin: 20rpx;
  border-radius: 50%;
}

.userinfo-nickname {
  color: #aaa;
}

.usermotto {
  margin-top: 150px;
}

.form-control {
  display: block;
  padding: 0 12px;
  margin-bottom: 5px;
  border: 1px solid #ccc;
}
.all{
  width:7.5rem;
  height:1rem;
  background-color:blue;
}
.all:after{
  display:block;
  content:'';
  clear:both;
}
.left{
  float:left;
  width:3rem;
  height:1rem;
  background-color:red;
}

.right{
  float:left;
  width:4.5rem;
  height:1rem;
  background-color:green;
}
</style>
