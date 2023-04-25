<template>
  <div id="detail">
    <detail-nav-bar class="detail-nav"></detail-nav-bar>
    <scroll class="detail-content" ref="scroll">
      <detail-swiper :topImages="topImages"></detail-swiper>
      <detail-base-info :goods="goods"></detail-base-info>
      <detail-shop-info :shop="shop"></detail-shop-info>
      <detail-goods-info :detail-info="detailInfo" @imgLoad="detailImgLoad"/>
      <detail-param-info :param-info="paramInfo"></detail-param-info>
      <detail-comment-info :commentInfo="commentInfo"></detail-comment-info>
      <goods-list :goods="recommend"></goods-list>
    </scroll>
  </div>
</template>

<script>
import DetailNavBar from "@/views/detail/childrenConmponents/DetailNavBar";
import { getDetail, Goods, Shop,GoodsParam,getRecommend } from "network/detail";
import DetailSwiper from "@/views/detail/childrenConmponents/DetailSwiper";
import DetailBaseInfo from "@/views/detail/childrenConmponents/DetailBaseInfo";
import DetailShopInfo from "@/views/detail/childrenConmponents/DetailShopInfo";
import DetailGoodsInfo from '@/views/detail/childrenConmponents/DetailGoodsInfo';
import DetailParamInfo from '@/views/detail/childrenConmponents/DetailParamInfo';
import DetailCommentInfo from '@/views/detail/childrenConmponents/DetailCommentInfo'
import Scroll from "@/components/common/scroll/Scroll";
import GoodsList from '@/components/content/goods/GoodsList'
export default {
  name: "Detail",
  components: {
    DetailNavBar,
    DetailSwiper,
    DetailBaseInfo,
    DetailShopInfo,
    DetailGoodsInfo,
    DetailParamInfo,
    DetailCommentInfo,
    Scroll,
    GoodsList 
  },
  data() {
    return {
      iid: null,
      topImages: [],
      goods: {},
      shop: {},
      detailInfo:{},
      paramInfo:{},
      commentInfo:[],
      recommend:[]
    };
  },
  methods:{
    detailImgLoad(){
      this.$refs.scroll.refresh()
    }
  },
  created() {
    console.log(this.$route.params.iid);

    this.iid = this.$route.params.iid;
    getDetail(this.iid).then(res => {
      console.log(res);
      const data = res.result;
      this.topImages = res.result.itemInfo.topImages;
      this.goods = new Goods(
        data.itemInfo,
        data.columns,
        data.shopInfo.services
      );
      this.shop = new Shop(data.shopInfo);
      this.detailInfo = data.detailInfo;
      this.paramInfo =new GoodsParam(data.itemParams.info,data.itemParams.rule)
    
        this.commentInfo = data.rate.list
        console.log(this.commentInfo);   
    
    });
    getRecommend().then((res) => {
      console.log(res);
      
        this.recommend = res.data.list
  })
  }
};
</script>

<style scoper>
#detail {
  position: relative;
  z-index: 999;
  background-color: #fff;
  height: 100vh;
}
.detail-content {
  position: absolute;
  top: 44px;
  bottom: 49px;
  left: 0;
  right: 0;
}
.detail-nav {
  position: relative;
  top: 0;
  left: 0;
  right: 0;
  z-index: 11;
  background-color: #fff;
}
</style>