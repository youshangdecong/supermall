<template>
  <div class="wrapper" ref="wrapper">
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
import BScroll from "better-scroll";
export default {
  props: {
    probeType: {
      type: Number,
      default: 1
    },
    pullUpLoad: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      scroll: null
    };
  },
  // mounted(){
  //     this.scroll = new BScroll(this.$refs.wrapper,{
  //        click:true,
  //        scrollY: true,
  //     })
  //     // this.scroll.scrollTo(0,0)
  // },
  mounted() {
    this.scroll = new BScroll(this.$refs.wrapper, {
      click: true,
      //   scrollY: true,
      probeType: this.probeType,
      pullUpLoad: this.pullUpLoad
    });
    this.scroll.on("scroll", position => {
      // console.log(position);
      this.$emit("scroll", position);
    });
    this.scroll.on("pullingUp", () => {
      //   console.log("上啦加载更多");
      this.$emit("pullingUp");
    });
  },
  methods: {
    scrollTo(x, y, time) {
      this.scroll.scrollTo(x, y, time);
    },
    finishPullUp() {
      this.scroll.finishPullUp();
    },
    refresh() {
      console.log("----");
      this.scroll.refresh();
    }
  }
};
</script>

<style>
</style>