<template>
  <div class>
    <Header></Header>
    <div @click="share" class="share">
      分享
    </div>
    <div class="main">
      
      <div class="star">
        <div class="avatar">
          <img v-if="!!avatar" :src="avatar" alt="">
          <img v-else src="../assets/img/avatar.png" alt="">
        </div>
        <div class="nickname">
          塔罗少年
        </div>
        <div class="img">
          <img :src="src" alt />
        </div>
        <div class="title">{{res.title}}</div>
        <div class="des" v-html="res.content">
          <!-- Buying the right telescope to take your love of astronomy to the next level is a big next step in the development of your passion for the stars. In many ways, it is a big step from someone who is just fooling around with astronomy to a serious student of the science. But you and I both know that there is still another big step after buying a telescope before you really know how to use it. -->
        </div>
      </div>
    </div>
    <Footer></Footer>
     <van-popup position="bottom"  v-model="show">
      <div class="popup">
        <div class="top">
          <!-- <div class="colse">关闭</div> -->
          <!-- <a href=""></a> -->
          <!-- <a href="" class="download">下载</a> -->
          
        </div>
        <span @click="show=false" class="cha iconfont icon-cha"></span>
        <div class="img-box">
          <img class="share-img" :src="urlImg" alt="">
          
        </div>
      </div>
    </van-popup>
  </div>
</template>

<script>
import Header from "../components/Header";
import Footer from "../components/Footer";
import html2canvas from "html2canvas";
export default {
  // props: {
  //   id: {}
  // },
  computed:{
    avatar(){
      return localStorage.getItem('avatar') 
    },
  },
  data() {
    return {
      res: {},
      src: "",
      show:false,
      urlImg:'',
    };
  },
  methods: {
    share(){
      this.show = true
      // 想要保存的图片节点

      html2canvas(document.querySelector(".star"), {
          allowTaint: false,
          useCORS: true
        }).then(canvas => { 
          console.log(canvas.toDataURL())

          this.urlImg = canvas.toDataURL(); 
        }); 
    },
    async getCardDetail() {
      const res = await this.$http.get(`card/record/day`);
      if (!res.data) {
        // this.$router.push
      }
      this.res = res.data;
      // this.$nextTick(()=>{
      this.src = this.res.icon;
      // })
      // this.save()
      console.log(this.src);
      console.log(res.data);
    }
    // async save(){
    //   const res = await this.$http.post(`card/record/day/create`,{card_id:this.id});
    //   // this.res = res.data;
    //   if(res.code==200){
    //     alert('保存成功')
    //   }else{
    //     alert(res.msg)
    //   }
    // },
  },
  mounted() {
    this.getCardDetail();
  },
  components: {
    Header,
    Footer
  }
};
</script>
<style>
.des img {
  width: 100% !important;
}
.ql-align-center img {
  width: 100%;
}
</style>

<style  lang="scss"  scoped>
.img-box{
  width: 100vw;
  img{
    width: 100vw;
  }
}
.popup{
  background:rgba(51,20,115,1);
  .icon-cha{
        color: #ADA7C1;
        font-size: 40px;
        position: absolute;
        top:2px;
        right: 32px;
      }
  .top{
    background: #400e8d;
    display: flex;
    position: relative;
    
    div,a{
      flex:1;
      text-align: center;
      font-size: 32px;
      line-height: 64px;
      color:#fff;
    }
  }
}
.main {
  background: #270e3b;
  padding-top: 160px;
  padding-bottom: 100px;
  overflow: auto;
  
  .star {
    .avatar{
      position: absolute;
      width: 140px;
      height: 140px;
      top: -70px;
      left: 0;
      right: 0;
      margin: 0 auto;
      border-radius: 50%;
      img{
        width: 100%;
        height: 100%;
        border-radius: 50%;
      }
    }
    .nickname{
      font-size: 32px;
      color: #fff;
      line-height: 32px;
      text-align: center;
    }
    width: 630px;
    height: calc(100vh - 190px - 110px);
    margin-left: 60px;
    background: linear-gradient(
      360deg,
      rgba(239, 222, 252, 0.04) 0%,
      rgba(251, 235, 255, 0.24) 100%
    );
    img {
      width: 100%;
    }
    border-radius: 20px;
    // opacity: 0.76;  写上这个好像name这里有模糊感
    position: relative;
    padding: 100px 30px;
    .img {
      width: 220px;
      height: 220px;
      margin: 36px auto 20px;
    }
    .title {
      text-align: center;
      height: 40px;
      line-height: 40px;
      font-size: 40px;
      color: #fff;
    }
    .des {
      font-size: 28px;
      color: #fff;
      line-height: 160%;
      padding-bottom: 400px;
      img {
        width: 100%;
      }
    }
  }
}
.des {
  font-size: 28px;
  color: #fff;
  line-height: 160%;
  p img {
    width: 100% !important;
  }
}
.rotate-section {
  height: 545px;
  padding: 40px 0;
  // background: #270E3B;
  .rotate-img {
    margin-left: calc(50vw - 232.5px);
    width: 465px;
    height: 465px;
    background: cornflowerblue;
  }
}
.share{
  position: absolute;
  top: 20px;
  right: 40px;
  color: #fff;
  font-size: 32px;
  line-height: 32px;
  padding:10px 25px;
  border-radius: 26px;
  background-color: #9237a8;
}
.star-cards {
  padding: 0 30px;
  // height: calc(100vh - 110px - 545px);
  overflow-y: scroll;
  // background: #270E3B;
  .card-item {
    padding: 32px;
    display: flex;
    background: linear-gradient(
      360deg,
      rgba(0, 0, 0, 0.9) 0%,
      rgba(0, 0, 0, 0.17) 100%
    );
    border-radius: 16px;
    opacity: 0.8;
    margin-bottom: 30px;
    &.on {
      background: linear-gradient(
        360deg,
        rgba(217, 80, 255, 0.09) 0%,
        rgba(212, 75, 250, 0.5) 100%
      );
    }
    .card-icon {
      height: 180px;
      width: 180px;
      img {
        width: 100%;
        height: 100%;
      }
    }
    .card-des {
      flex: 1;
      height: 180px;
      margin-left: 10px;
      .star-name {
        font-size: 36px;
        line-height: 50px;
        margin-top: 10px;
        color: #fff;
      }
      .star-des {
        font-size: 28px;
        line-height: 40px;
        margin-top: 0px;
        color: #9452a3;
      }
      .star-date {
        font-size: 28px;
        line-height: 40px;
        margin-top: 25px;
        color: #fcdfc9;
      }
    }
    .card-button {
      margin-top: 45px;
      .button-icon {
        width: 48px;
        height: 48px;
        margin: 0px 16px 10px;
        background: url("../assets/img/card-button.png") no-repeat;
        background-size: contain;
      }
      .button-txt {
        font-size: 26px;
        line-height: 38px;
        color: #d27ae7;
      }
    }
  }
}
</style>