<template>
  <div id="home">
    <nav-bar class="home-nav">
      <div slot="center">购物街</div>
    </nav-bar>
    <home-swipe :banners="banners"></home-swipe>
    <home-recommend-view :recommends="recommends"></home-recommend-view>
    <home-feature-view></home-feature-view>
    <tab-control class="tab-control" :titles="['流行','新款','精选']" @tabClick="getTabClick"></tab-control>
<!--    <goods-list :goods="goods[showGoods].list"></goods-list>-->


    <ul>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>
      <li>1111</li>


    </ul>

  </div>
</template>

<script>
  import HomeSwipe from "./childComps/HomeSwipe";
  import HomeRecommendView from "./childComps/HomeRecommendView";
  import HomeFeatureView from "./childComps/HomeFeatureView";

  import NavBar from "components/common/navbar/NavBar";
  import TabControl from "components/content/tabControl/TabControl";
  import GoodsList from "components/content/goods/GoodsList";

  import {getHomeMultidata, getHomeGoods} from "network/home";


  export default {
    name: "Home",
    components: {
      NavBar,
      HomeSwipe,
      HomeRecommendView,
      HomeFeatureView,

      TabControl,
      GoodsList

    },
    //用于保存请求过来的数据
    data() {
      return {
        //result:null
        banners: [],
        recommends: [],
        goods: {
          //page:数据现在加载了几页,默认最开始加载0页，list,数据现在加载了多少条
          'pop': {page: 0, list: []},
          'news': {page: 0, list: []},
          'sell': {page: 0, list: []},
        },
        currentType: 'pop'

      }
    },
    computed:{
      showGoods(){
        return this.goods[this.currentType].list
      }
    },
    //当首页组件创建好之后就发送网络请求,请求首页的所有数据
    created() {
      //created写主要的逻辑，比如写我调用了哪个方法，至于方法怎么实现的就放在方法里
      //如果方法里的方法名和方法里的重名，再create里调用的时候要加this
      //1.请求多个数据
      this.getHomeMultidata()
      //2.请求商品数据
      this.getHomeGoods('pop')
      this.getHomeGoods('new')
      this.getHomeGoods('sell')
    },
    methods: {
      //方法里写主要做的事情
      //时间监听相关的方法
      getTabClick(index) {
        // console.log(index)
        switch (index) {
          case 0:
            this.currentType = 'pop'
            break
          case 1:
            this.currentType = 'new'
            break
          case 2:
            this.currentType = 'sell'
            break


        }
      },
      //网络请求相关的方法
      getHomeMultidata() {
        getHomeMultidata().then(res => {
          //console.log(res);
          //this.result = res
          this.banners = res.data.banner.list;
          this.recommends = res.data.recommend.list;
        })
      },
      getHomeGoods(type) {
        const page = this.goods[type].page + 1
        getHomeGoods(type, page).then(res => {
          console.log(res);
          //res.data.list取到数组,然后用push存到一个地方
          this.goods[type].list.push(...res.data.list)
          this.goods[type].page += 1
        })
      },
    }


  }

</script>

<style scoped>
  #home {
    padding-top: 43.6px;
  }

  .home-nav {
    background-color: var(--color-tint);
    color: #fff;
    position: fixed;
    left: 0;
    right: 0;
    top: 0;
    z-index: 9;
  }

  .tab-control {
    position: sticky;
    top: 43.6px;
  }
</style>
