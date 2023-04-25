<template>
   <div class="tab-control">
       <div v-for="(item,index) in titles" :key="item.index " 
       class="tab-control-item" :class="{active:index==currentIndex}" @click="btnClick(index)">
          <span> {{item}}</span>
       </div>
   </div>
</template>

<script>
export default {
    props:{
        titles:{
            type:Array,
            default(){
                return[]
            }
        }
        
    },
    data(){
        return {
            currentIndex:0
        }
    },
    methods:{
        btnClick(index){
           this.currentIndex = index ;
           this.$emit('tabClick',index)
        }
    }

}
</script>

<style>
    .tab-control {
        display: flex;
        text-align: center;
        font-size: 16px
    }
    .tab-control-item {
        flex: 1;
        height: 40px;
        line-height: 40px;
    }
    .active {
        color:blue;
           
    }
     .active span {
      border-bottom: 2px solid blue
     }
</style>