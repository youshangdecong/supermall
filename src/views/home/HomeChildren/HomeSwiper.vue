<template>
     <swiper>
        <swiper-item v-for="item in banners" :key="item.id">
            <a :href="item.link">
              <img :src="item.image" alt="" @load="imgLoad">
            </a>
        </swiper-item>
      </swiper>
</template>

<script>
import { Swiper, SwiperItem } from 'components/common/swiper'
export default {
    props:{
        banners:{
            type:Array,
            default(){
                return []
            }
        }
    },
    data(){
        return {
            load:false
        }
    },
    components:{
         Swiper,
      SwiperItem 
    },
    methods:{
        imgLoad(){
            if (!this.isLoad) {
                this.$emit('swiperImgLoad')
                this.isLoad = true
            }
        }
    }
}
</script>

<style>

</style>