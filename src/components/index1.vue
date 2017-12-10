<template>
  <div>
    <mu-appbar title="Title">
      <mu-icon-button icon="menu" slot="left"/>
      <mu-flat-button label="expand_more" slot="right"/>
      <mu-icon-button icon="expand_more" slot="right"/>
    </mu-appbar>
    <div class="icons">
      <!--<mu-list-item>-->
        <!--<mu-avatar slot="left" :src="indexPages.icon"/>-->
      <!--</mu-list-item>-->
      <!--<mu-list-item>-->
        <!--<mu-avatar slot="left" :src="indexPages.icon"/>-->
      <!--</mu-list-item>-->
    </div>
    <mu-tabs :value="activeTab" @change="handleTabChange">
      <mu-tab value="tab1" title="宠物"/>
      <mu-tab value="tab2" title="美食"/>
      <mu-tab value="tab3" @active="handleActive" title="美女"/>
    </mu-tabs>
    <div v-if="activeTab === 'tab1'">
      <div class="avatar">
        <mu-list-item title="张三" disabled>
          <mu-avatar slot="left" :src="indexPages.icon"/>
        </mu-list-item>
      </div>
      <div class="image-dec">
        {{indexPages.email}}
      </div>
      <div class="image-context">
        <mu-card>
        <mu-card-media >
          <img :src="images[0].imgs[0].url" />
        </mu-card-media>
          <mu-card-media >
            <img :src="images[0].imgs[0].url" />
        </mu-card-media>
        </mu-card>
      </div>
    </div>
    <div v-if="activeTab === 'tab2'">
      <h2>popular</h2>
      <p>
        这是第二个 tab
      </p>
    </div>
    <div v-if="activeTab === 'tab3'">
      <h2>selected</h2>
      <p>
        这是第三个 tab
      </p>
    </div>
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
        images:{},
        tranform: this.$store.state.tranform,
        menushow: true,
        headtitle: "发现",
        publictitle: "发现美好",
        ymd: '',
        id: this.$route.query.id,
        sex:["女","男"],
        activeTab: 'tab1',
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
      });
      this.$http.get('/api/judgement/image').then((success) => {
        console.log(success.body.result)
        this.tranform = false;
        // 由于请求成功返回的是Promise对象，我们要从success.body拿到数组
        this.images = success.body.result;
      }, (error) => {
        console.log(error)
      })
    },
    methods: {
      handleTabChange (val) {
        this.activeTab = val
      },
      handleActive () {
        window.alert('tab active')
      }
    },
  }
</script>

<style lang="less" scoped>
  @import './../assets/css/public.css';
  @import "./../assets/css/style.css";
  .mu-appbar{
    background-color: mediumslateblue;
  }
  .icons{
    background-color: mediumslateblue;
    height: 180px;
  }
  .avatar{
    margin-left: 2%;
    margin-top: 2%;
  }
  .image-dec{
    margin-left: 6%;
  }
  .mu-card{
    box-shadow: none;
  }
  .mu-card-media>img{
    border-radius: 30px;
  }
  .mu-card-media{
    margin: 30px;
  }
  .mu-card-media-title{
    display: none;
  }
  .image-context{

  }
  .mu-tabs {
    background-color: #ffffff;
  }
  .mu-tab-link{
    color: mediumslateblue;
  }
  .mu-tab-active{
    color: black;
  }
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
