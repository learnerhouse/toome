<template>
    <div>
      <backbar></backbar>
      <spinner v-if='tranform'></spinner>
      <div v-if='!tranform' class="detailMargin backAddFont">
        <mu-sub-header class="detailTitle">{{ detailBody.title }}</mu-sub-header>
        <mu-card-title :subTitle="ymd > detailBody.createdAt.substring(0,10) ? detailBody.createdAt.substring(0,10):detailBody.createdAt.substr(11,5)"/>
        <mu-content-block class="detailContent">
          <mu-card-media>
            <img :src="detailBody.CoverMap.url">
          </mu-card-media>
          <br>
          {{ detailBody.content }}
        </mu-content-block>
      </div>
    </div>
</template>
<style lang="less" >
  @import './../assets/css/public.css';
  .detailTitle{
    font-size: 25px;
    font-weight: bold;
  }
  .detailContent{
    font-size: 16px;
  }

</style>
<script type="text/ecmascript-6">
  import backbar from './public/backBar.vue'
  import spinner from './public/spinner.vue'
    export default{
      data(){
        return{
          tranform: this.$store.state.tranform,
          id: this.$route.params.id,
          detailBody:[],
          ymd:'',
        }
      },
      created() {
        this.$http.get('https://api.leancloud.cn/1.1/classes/explore/'+this.id ).then((success) => {
          this.tranform = false;
          this.detailBody = success.body;
          this.newDate();
          console.log("https://api.leancloud.cn/1.1/classes/explore/：")
          console.log(JSON.stringify(success.body.results))
        }, (error) => {
          console.log(error)
        })
      },
      methods:{
        //时间格式处理
        newDate(){
          let myDate = new Date();
          let year = 1900+myDate.getFullYear();
          let month = myDate.getMonth()+1;
          if(month<10){
            month = "0" + month
          }
          let day = myDate.getDate();
          if(day<10){
            day = "0" + day
          }
          this.ymd = year+"-"+month+"-"+day;
          // console.log(this.ymd);
        }
      },
      components:{
        backbar,
        spinner
      }
    }
</script>
