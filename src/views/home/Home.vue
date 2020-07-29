<template>
  <div id="home">
    <nav-bar class="home-nav">
      <div slot="center">购物街</div>
    </nav-bar>
    <scroll class="content" ref="scroll" :probeType="3" @scroll="contentScroll" :pull-up-load="true" @pullUpLoad="loadMore">
      <home-swiper :banners="banners"></home-swiper>
      <home-recommend-view :recommends="recommends"></home-recommend-view>
      <feature></feature>
      <tab-control class="tab-control" :titles="['流行','新款','精选']" @tabClick="tabClick"></tab-control>
      <goods-list :goods="goods[currentType].list"></goods-list>
    </scroll>
     <back-top @click.native="backClick()" v-show="isShow"></back-top>
  </div>
</template>

<script>
import NavBar from "components/common/navbar/NavBar";
import HomeSwiper from "./HomeChildren/HomeSwiper";
import HomeRecommendView from "./HomeChildren/HomeRecommendView";
import Feature from "./HomeChildren/Feature";
import TabControl from "components/content/tabControl/TabControl";
import GoodsList from "components/content/goods/GoodsList";
import { getHomeMultidata, getHomeGoods } from "@/network/home.js";
import Scroll from '@/components/common/scroll/Scroll'
import backTop from '@/components/content/backtop/BackTop'
export default {
  components: {
    NavBar,
    HomeSwiper,
    HomeRecommendView,
    TabControl,
    Feature,
    GoodsList,
     Scroll,
     backTop
  },
  data() {
    return {
      banners: [],
      recommends: [],
      goods: {
        pop: { page: 0, list: [] },
        new: { page: 0, list: [] },
        sell: { page: 0, list: [] }
      },
      currentTypeArray: ["pop", "new", "sell"],
      currentType: "pop",
      isShow:false
    };
  },
  created() {
    this.getHomeMultidata();
    this.getHomeGoods("pop");
    this.getHomeGoods("new");
    this.getHomeGoods("sell");
  },
  methods: {
    //事件监听
    tabClick(index) {
      // console.log(index);
      this.currentType = this.currentTypeArray[index];
      console.log(this.currentType);
    },
    backClick(){
      this.$refs.scroll.scrollTo(0,0,1000);
      console.log(111);
      
    },
    contentScroll(position){
      // console.log(position);
      this.isShow = (-position.y) > 1000 
    },
    loadMore(){
      console.log(233);
      this.getHomeGoods(this.currentType)
      this.$refs.scroll.scroll.refresh()
    },
    // 网络请求
    getHomeMultidata() {
      getHomeMultidata().then(res => {
        this.banners = res.data.banner.list;
        this.recommends = res.data.recommend.list;
      });
    },
    getHomeGoods(type) {
      const page = this.goods[type].page + 1;
      getHomeGoods(type, page).then(res => {
        this.goods[type].list.push(...res.data.list);
        this.goods[type].page += 1;
        this.$refs.scroll.finishPullUp()
      });
    }
  }
};
</script>

<style scoped>
#home {
  /* padding-top: 44px; */
  height: 100vh;
  position: relative;
}
.home-nav {
  background-color: red;
  color: #fff;
  position: fixed;
  left: 0;
  right: 0;
  top: 0;
  z-index: 999;
}
.tab-control {
  position: sticky;
  top: 44px;
  z-index: 999;
  background-color: #eee;
}
.content {
  /* height: calc(100%-93px);
  overflow: hidden; */
  	overflow: hidden;
		position: absolute;
		left: 0;
		right: 0;
		top: 44px;
		bottom: 49px;
}
</style>