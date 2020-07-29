<template>
  <div class="recommend">
      <div v-for="item in recommends" :key="item.index" class="recommend-item">
          <a :href="item.link">
              <img :src="item.image" alt="">
              <div>{{item.title}}</div>
          </a>
      </div>
  </div>
</template>

<script>
export default {
    props:{
        recommends:{
              type:Array,
             default(){
                return []
            }
        }
    }
}
</script>

<style>
    .recommend {
        display: flex;
        width: 100%;
        text-align: center;
        font-size: 12px;
        margin-top: 10px;
        padding: 10px 0 15px;
        border-bottom: 5px solid #eee
    }
    .recommend-item {
        flex:1;
    }
      .recommend-item img{
          width: 80px;
          height: 80px;
      }
</style>