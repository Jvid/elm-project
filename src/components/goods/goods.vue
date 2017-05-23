<template>
  <div class="goods">
    <div class="menu-wrapper">
      <ul>
        <li v-for="item in goods" class="menu-item">
          <span class="text border-1px">
            <span v-show="item.type>0" class="icon" :class="classMap[item.type]"></span>
            {{item.name}}
          </span>
        </li>
      </ul>
    </div>
    <div class="foods-wrapper">
      
    </div>
  </div>

</template>

<script>
  const ERR_OK = 0;
export default {
  props: {
    seller: {
      type:Object
    }
  },
  data() {
   return {
     goods:{}
   }
  },
  created() {
    this.classMap = ['decrease','discount','special','invoice','guarantee'];
    this.$http.get('/api/goods').then((response) => {
      response = response.body;
      if(response.errno === ERR_OK){
//        console.log(response.data);
        this.goods = response.data;
      }
    })
  }
}
</script>

<style lang="scss" scoped>
  @import "../../common/css/mixin";
.goods{
  display: flex;
  overflow: hidden;
  position:absolute;
  top:174px;
  bottom:46px;
  width:100%;
  .menu-wrapper{
    flex: 0 0 80px;
    width: 80px;
    background:#f3f5f7;
    .menu-item{
      display: table;
      height: 54px;
      width: 56px;
      line-height: 14px;
      padding:0 12px;
      .icon{
        display: inline-block;
        width: 12px;
        height: 12px;
        vertical-align:top;
        margin-right: 2px;
        background-size: 12px 12px;
        background-repeat: no-repeat;
        &.decrease{
         @include bg-image('decrease_3');
         }
        &.discount{
         @include bg-image('discount_3');
         }
        &.guarantee{
         @include bg-image('guarantee_3');
         }
        &.invoice{
         @include bg-image('invoice_3');
         }
        &.special{
         @include bg-image('special_3');
         }
      }
      .text{
        display: table-cell;
        width: 56px;
        vertical-align: middle;
        font-size:12px;
        @include border-1px(rgba(7,17,27,0.1))
      }
    }
  }
  .foods-wrapper{
    flex:1;
  }
}
</style>
