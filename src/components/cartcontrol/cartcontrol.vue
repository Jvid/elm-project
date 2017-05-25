<template>
  	<div class="cartcontrol">
  		<transition name="move">
  			<div class="cart-decrease" @click="decreaseCart($event)" v-show="food.count>0">
  				<span class="inner icon-remove_circle_outline"></span>
  			</div>
  		</transition>
  		<transition>
  			<div class="cart-count" v-show="food.count>0">{{food.count}}</div>
  		</transition>
  		<div class="cart-add icon-add_circle" @click="addCart($event)"></div>
  	</div>
</template>

<script type="text/ecmascript-6">
import Vue from 'vue';
export default {
	props: {
		food: {
			type: Object
		}
	},
	created() {
		// console.log(this.food)
	},
	methods:{
		addCart(event) {
			if(!event._constructed) {
				return;
			}
			if(!this.food.count){
				Vue.set(this.food,'count',1);
			}else{
				this.food.count++
			}
		},
		decreaseCart(event) {
			if(!event._constructed) {
				return;
			}
			if(!this.food.count){
				Vue.set(this.food,'count',0);
			}else{
				this.food.count--
			}
		}
	}
}
</script>

<style lang="scss" scoped>
	.cartcontrol{
		font-size: 0;
		.cart-decrease{
			display: inline-block;
			padding: 6px;
			// transform: translate3D(0,0,0) rotateZ(0);
			transition:all linear .5s;
			.inner{
				display: inline-block;
				font-size: 24px;
				line-height: 24px;
				color:rgb(0,160,220);
			}
		}
		.cart-decrease{

		}
		.cart-count{
			display: inline-block;
			vertical-align: top;
			width: 12px;
			padding-top: 6px;
			line-height: 24px;
			text-align:center;
			font-size: 10px;
			color: rgb(147,153,159);
		}
		.cart-add{
			display: inline-block;
			padding: 6px;
			font-size: 24px;
			line-height: 24px;
			color:rgb(0,160,220)
		}
	}
.move-enter-active,.move-leave{
  opacity: 1;
  transform: translateX(0) rotate(0);
  // transform: translate3D(0,0,0) rotateZ(0);
}
.move-enter,.move-leave-active{
  opacity: 0;
  transform: translateX(24px) rotate(180deg);
  // transform: translate3D(24px,0,0) rotateZ(180deg);
}
</style>