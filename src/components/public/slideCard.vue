<template>
  <div class="swiper">
    <swiper class="swiperTop" :options="swiperOption">
      <!--<swiper-slide class="slide" v-for = "page in indexPages">-->
        <!--<div class="slideImg">-->
          <!--&lt;!&ndash;<img src="../../assets/image/slide1.jpeg" />&ndash;&gt;-->
          <!--<img :src='page.image' />-->
          <!--&lt;!&ndash;<img src="https://images.simpletour.com/simpletour/images/wechat_banner/45354e74a7dfda4177e081fbb188fc11.jpg!wechatQ3640160" />&ndash;&gt;-->
        <!--</div>-->
      <!--</swiper-slide>-->

      <swiper-slide class="slide">
        <div class="slideImg">
          <img src="../../assets/image/blueSky.jpg" />
          <!--<img src="https://images.simpletour.com/simpletour/images/wechat_banner/45354e74a7dfda4177e081fbb188fc11.jpg!wechatQ3640160" />-->
        </div>
      </swiper-slide>

      <div class="swiper-pagination" slot="pagination"></div>
    </swiper>
  </div>
</template>
<style lang="less" scoped>
  .swiperTop{
    margin-top: 100px;
    margin-left: 10px;
    margin-right: 10px;
  }
  .slide{
    width: 100%;
    height: 210px;
    /*border-radius: 25px;*/
    background: #dedede;
  }
  .slideImg img{
    width:100%;
    height: 210px;
    /*border-radius: 25px;*/
  }
</style>
<script type="text/ecmascript-6">
  export default{
    data() {
      return {
        swiperOption: {
          pagination: '.swiper-pagination',
          paginationClickable: true
        }
      }
    },
    create(){

    },
    props:['indexPages']
  }
</script>
