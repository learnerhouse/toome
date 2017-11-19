<template>
  <div>
    <publicheader :menushow="menushow" :headtitle="headtitle" ></publicheader>
    <mu-card>
      <mu-card-header :title="indexPages.realName" :subTitle="sex[indexPages.sex]">
        <mu-avatar :src="indexPages.icon" slot="avatar"/>
      </mu-card-header>
      <mu-card-media :title="image" subTitle="Image Sub Title">
        <img src="../assets/image/blueSky.jpg" />
      </mu-card-media>
      <mu-card-title title="Content Title" subTitle="Content Title"/>
      <mu-card-text>
        散落在指尖的阳光，我试着轻轻抓住光影的踪迹，它却在眉宇间投下一片淡淡的阴影。
        调皮的阳光掀动了四月的心帘，温暖如约的歌声渐起。
        似乎在诉说着，我也可以在漆黑的角落里，找到阴影背后的阳光，
        找到阳光与阴影奏出和谐的旋律。我要用一颗敏感赤诚的心迎接每一缕滑过指尖的阳光！
      </mu-card-text>
      <mu-card-actions>
        <mu-flat-button label="Action 1"/>
        <mu-flat-button label="Action 2"/>
      </mu-card-actions>
    </mu-card>
  </div>

</template>


<script type="text/ecmascript-6">
  import swiper from './public/swiper'
  import spinner from './public/spinner'
  import publicheader from './public/publicHeader'
  import publictitle from './public/publicTitle'
  import slidecard from './public/slideCard.vue'
  export default {
    data() {
      return {
        indexPages: {},
        tranform: this.$store.state.tranform,
        menushow: true,
        headtitle: "发现",
        publictitle: "发现美好",
        ymd: '',
        id: this.$route.query.id,
        sex:["女","男"],
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
      this.$http.get('/api/toome/index/userDetail?id=test').then((success) => {
        console.log(success.body.result)
        this.tranform = false;
        // 由于请求成功返回的是Promise对象，我们要从success.body拿到数组
        this.indexPages = success.body.result;
      }, (error) => {
        console.log(error)
      })
    },
  }
</script>

<style lang="less" scoped>
  @import './../assets/css/public.css';
  @import "./../assets/css/style.css";
  .mu-card-header {
    margin-top: 14%;
    padding: 2%;
  }
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

</style>
