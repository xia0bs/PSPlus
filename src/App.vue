<template>
  <div id="app">
    <div class="swiper-container">
      <ul class="swiper-wrapper content">
        <li class="swiper-slide"
            v-for="(item,index) in items"
            :key="index"
            :class="{'active':index%2 !== 1}"
            :style="{backgroundImage: 'url(' + item.attributes['thumbnail-url-base'] + ')', backgroundRepeat:'no-repeat', backgroundPosition:'center center', backgroundSize:'cover'}">
            <div class="cover"></div>
            <p>{{item.attributes.name}}</p>
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
  import Swiper from 'swiper';
  export default {
  name: 'App',
  data () {
    return {
      items:{}
    }
  },
  mounted () {
    this.axios.get('api/valkyrie-api/zh/HK/19/container/STORE-MSF86012-PLUS_FTT_CONTENT', {
      params: {
        size: 30,
        bucket: 'games',
        start: 0
      }
    })
      .then((res)=>{
        this.items = res.data.included

        this.$nextTick(() => {
          new Swiper('.swiper-container', {
            slidesPerView: 2.3,
            spaceBetween: 10,
            freeMode: true
          });
        })
      })
      .catch(function (error) {
        console.log(error);
      });
  },
  methods: {

  }
}
</script>
<style>
@import url('../static/swiper.min.css');
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  max-width: 100%;
  height: 140px;
  padding: 10px;
}
*{
  padding: 0;
  margin: 0;
  list-style: none;
}
.swiper-container{
  height: 100%;
}
.swiper-slide{
  border-radius: 10px;
  text-align: center;
  font-size: 14px;
  position: relative;
  overflow: hidden;
}
.swiper-slide a{
  height: 140px;
  display: block;
}
.swiper-slide p{
  position: absolute;
  bottom: 5px;
  left: 0;
  right: 0;
  margin: auto;
  padding: 0 5px 0;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  color: #fff;
}
.cover{
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 30px;
  background: rgba(0,0,0,.6);
}
.active{
  display: none;
}
</style>
