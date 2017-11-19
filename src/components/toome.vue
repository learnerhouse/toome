<template>
  <div class="toomeindex">
    <!--<spinner v-if='tranform'></spinner>-->
    <div>
      <publicheader :menushow="menushow" :headtitle="headtitle" ></publicheader>
    </div>

    <div class="avatar-icon">
      <img src="../assets/image/avatar.png"/>
    </div>
    <slidecard :indexPages ="indexPages"></slidecard>

    <div class="choose">
        <!--<span class="icon-indexcross"></span>-->
        <!--<span class="icon-indexheart"></span>-->

      <div class="button-icon">
        <img src="../assets/image/cross.png"/>
        <img src="../assets/image/tumi.png"/>
        <img src="../assets/image/like.png"/>
      </div>

    </div>

  </div>
</template>


<script type="text/ecmascript-6">
  import swiper from './public/swiper'
  import spinner from './public/spinner'
  import publicheader from './public/publicHeader'
  import publictitle from './public/publicTitle'
  import slidecard from './public/slideCard.vue'

  export default{
    data() {
      return {
        indexPages: [],
        tranform: this.$store.state.tranform,
        menushow: true,
        headtitle: "发现",
        publictitle: "发现美好",
        ymd: '',
        id: this.$route.query.id,
      }
    },
    components: {
      spinner,
      slidecard,
      publicheader,
      publictitle,
    },
    created() {
    // 在main.js里导入并使用vue-resource之后，就可以通过this.$http来使用vue-resource了，这里我们用到了get方法
    this.$http.get('/api/indexPages').then((success) => {
      console.log(success.body)
      this.tranform = false;
      // 由于请求成功返回的是Promise对象，我们要从success.body拿到数组
      this.indexPages = success.body.data.result;
      console.log(JSON.stringify(success.body.data.result))
    }, (error) => {
      console.log(error)
    })
    },
  }

</script>

<style lang="less" scoped>
  @import './../assets/css/public.css';
  @import "./../assets/css/style.css";
  .flexItem{
    width: 100%;
    height: 75px;
    background-color: #565645;
    text-align: center;
    line-height: 100px;
  }
  .flexItem img{
    width: 100%;
    height: 100%;
  }
  .indexContent{
    margin: 20px 0;
    background: #fff;
  }
  .cardImg{
    width: 100%;
    height: auto;
  }
  .choose{
    text-align: center;
    margin-top: 80px;
  }
  .icon-indexcross{
    font-size: 80px;
    color: #3d1e0d;
    margin-right: 80px;
  }
  .icon-indexheart{
    font-size: 80px;
    color: #3d1e0d;
  }
  .toomeindex{

  }
  .button-icon img{
    width: 30%;
    height: auto;
  }
  .avatar-icon{
    margin-top: 30px;
    margin-left: 10px;
  }
  .avatar-icon img{
    position: absolute;
    width: 20%;
    height: auto;
  }

</style>
