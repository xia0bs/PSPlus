<template>
  <div id="app">
    <div class="swiper-container">
      <ul class="swiper-wrapper content">
        <li class="swiper-slide"
            v-for="(item,index) in items"
            :key="index"
            :class="{'active':index%2 !== 1}"
            :style="{backgroundImage: 'url(' + item.attributes['thumbnail-url-base'] + '?w=248&h=248' + ')', backgroundRepeat:'no-repeat', backgroundPosition:'center center', backgroundSize:'cover'}">
            <div class="badge">
                <span>{{item.attributes.platforms[0]}}</span>
            </div>
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
        this.items = res.data.included;
        this.$nextTick(() => {
          new Swiper('.swiper-container', {
            slidesPerView: 'auto',
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
  height: 160px;
  -moz-user-select: none;
  -webkit-user-select: none;
  -ms-user-select: none;
  user-select: none;
  padding: 0 15px 0;
  -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
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
  width: 160px;
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
.badge{
    content:"";
    display:block;
    height:0;
    border-width:0 15px 15px;
    border-style:none solid solid;
    border-color:transparent transparent #ffe312;
    position:absolute;
    -moz-transform:rotate(-45deg);/*FF浏览器*/
    -webkit-transform:rotate(-45deg);/*chrome浏览器*/
    -o-transform:rotate(-45deg);/*oprea浏览器*/
    -ms-transform:rotate(-45deg);/*IE浏览器*/
    left: -18px;
    top: 17px;
    width: 56px;
    opacity: .9;
}
.badge span{
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    font-size: 12px;
    color: #472400;
    font-weight: bold;
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
