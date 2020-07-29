<template>
    <div class="tab-item" @click="itemClick">
        <div v-if="!isActive"> <slot name="item-icon"></slot></div>
        <div v-else> <slot name="item-icon-active"></slot></div>
        <div :style="styleActive"><slot name="item-text"></slot></div>
    </div>
</template>

<script>
export default {
    props:{
        path:String,
        activeColor:{
            type:String,
            default:'red'
        }
    },
    data(){
        return {
            // isActive:flase
        }
    },
    computed:{
        isActive(){
           return this.$route.path.indexOf(this.path) !== -1
        },
        styleActive(){
            return  this.isActive? {color:this.activeColor} : {}
        }
    },
    methods:{
        itemClick(){
            this.$router.replace(this.path)
    
        }
    }
}
</script>

<style>
 .tab-item {
  flex: 1;
  text-align: center;
  height: 49px;
  font-size: 12px;
}
.tab-item img {
    width:24px;
    height: 24px;
    margin-top: 3px;
    vertical-align: middle
}   
     
</style>