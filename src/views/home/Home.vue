<template>
  <div id="home">
    <nav-bar class="home-nav">
      <div slot="center">购物街</div>
          </nav-bar>
    <home-swipe :banners="banners"></home-swipe>
    <home-recommend-view :recommends="recommends"></home-recommend-view>
  </div>
</template>

<script>
  import NavBar from "components/common/navbar/NavBar";
  import HomeSwipe from "./childComps/HomeSwipe";
  import HomeRecommendView from "./childComps/HomeRecommendView";
  import {getHomeMultidata} from "network/home";



  export default {
    name: "Home",
    components: {
      NavBar,
      HomeSwipe,
      HomeRecommendView

    },
    //用于保存请求过来的数据
    data() {
      return {
        //result:null
        banners: [],
        recommends: []
      }
    },
    //当首页组件创建好之后就发送网络请求,请求首页的所有数据
    created() {
      //1.请求多个数据
      getHomeMultidata().then(res => {
        //console.log(res);
        //this.result = res
        this.banners = res.data.banner.list;
        this.recommends = res.data.recommend.list;
      })
    }

  }
</script>

<style scoped>
  .home-nav {
    background-color: var(--color-tint);
    color: #fff
  }
</style>
