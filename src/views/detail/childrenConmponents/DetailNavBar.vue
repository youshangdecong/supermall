<template>
  <nav-bar>
      <div slot="left" class="back" @click="backClick">
           <img src="~assets/images/fanhui.png" alt="">
      </div>
    <div slot="center" class="title">
       
        <div v-for="(item,index) in titles" :key="item.id" class="title-item" @click="titleClick(index)" :class="{active:index == cutter}">
            {{item}}
        </div>
    </div>
  </nav-bar>
</template>

<script>
import NavBar from "@/components/common/navbar/NavBar";
export default {
    components: {
    NavBar
  },
  data(){
      return {
          titles:['商品','参数','评论','推荐'],
          cutter:0
      }
  },
  methods:{
      titleClick(index){
          this.cutter = index
      },
      backClick(){
          this.$router.go(-1)
      }
  }
};
</script>

<style>
    .title {
        display: flex;
        font-size: 13px
    }
    .title-item {
        flex: 1
    }
    .active {
        color: blue
    }
    .back img{
        width: 30px;
        height: 30px;
        margin-top: 10px;
        margin-left: 5px;
    }
</style>