<template>
	<transition name="move">
		<div class="food" v-show="showFlag" ref="food">
			<div class="food-content">
				<div class="image-header">
					<img :src="food.image">
					<div class="back" @click="hide">
						<i class="icon-arrow_lift"></i>
					</div>
				</div>
				<div class="content">
					<h1 class="title">{{food.name}}</h1>
					<div class="detail">
						<span class="sell-count">月售{{food.sellCount}}</span>
						<span class="rating">好评率{{food.rating}}%</span>
					</div>
					<div class="price">
						<span class="now">￥{{food.price}}</span>
	                  	<span class="old" v-show="food.oldPrice">￥{{food.oldPrice}}</span>
					</div>
					<div class="cartcontrol-wrapper">
						<cartcontrol :food="food"></cartcontrol>	
					</div>
					<transition name="fade">
						<div class="buy" v-show="!food.count || food.count === 0" @click.stop.prevent="addFirst($event)">加入购物车</div>
					</transition>
				</div>
				<split v-show="food.info"></split>
				<div class="info" v-show="food.info">
					<h1 class="title">商品介绍</h1>
					<p class="text">{{food.info}}</p>
				</div>
				<split></split>
				<div class="rating">
					<h1 class="title">商品评价</h1>
					<ratingselect></ratingselect>
				</div>
			</div>
		</div>
	</transition>
</template>

<script type="text/ecmasript-6">
import BScroll from "better-scroll";
import Vue from 'vue';
import cartcontrol from "@/components/cartcontrol/cartcontrol";
import split from "@/components/split/split";
import ratingselect from "@/components/ratingselect/ratingselect";

	export default {
		props: {
			food: {
				type: Object
			}
		},
		data() {
			return {
				showFlag: false
			}
		},
		methods: {
			show() {
				this.showFlag = true;
				this.$nextTick(() => {
					if(!this.scroll){
						this.scroll = new BScroll(this.$refs.food,{
							click:true
						})
					}else{
						this.scroll.refresh();
					}
				})
			},
			hide() {
				this.showFlag = false
			},
			addFirst(event) {
				if(!event._constructed){
			       return;
			    }
			    Vue.set(this.food,'count',1)
			}
		},
		components: {
			cartcontrol,
			split,
			ratingselect
		}
	}
</script>

<style lang="scss" scoped>
	.food{
		position: fixed;
		left: 0;
		top: 0;
		bottom: 48px;
		z-index: 30;
		width: 100%;
		background: #fff;
		transition: all ease .3s;
	}
	.image-header{
		position: relative;
		width: 100%;
		height: 0;
		padding-top: 100%;
		img{
			position: absolute;
			top: 0;
			left: 0;
			width: 100%;
			height: 100%;
		}
		.back{
			position: absolute;
			top: 10px;
			left: 0;
			border-radius:40px;
			background: rgba(0,0,0,.2);
			.icon-arrow_lift{
				display: block;
				padding: 10px;
				font-size: 20px;
				color: #fff;
			}
		}
	}
	.content{
		padding: 18px;
		position: relative;
		.title{
			line-height: 14px;
			font-size: 14px;
			margin-bottom: 8px;
			font-weight: 700px;
			color: rgb(7,17,27)
		}
		.detail{
			margin-bottom: 18px;
			line-height: 10px;
			height: 10px;
			font-size: 0;
			.sell-count,.rating{
				font-size: 10px;
				color: rgb(147,153,129);
			} 
			.sell-count{
				margin-right: 12px;
			}
		}
		.price{
			font-weight: 700;
			line-height: 24px;
			font-size: 0;
			.now{
				margin-right: 8px;
				font-size: 14px;
				color: rgb(240,20,20);
			}
			.old{
				text-decoration: line-through;
				font-size: 10px;
				color: rgb(147,153,159);
			}
		}
		.cartcontrol-wrapper{
			position: absolute;
			right: 12px;
			bottom: 12px;
		}
		.buy{
			position: absolute;
			right: 18px;
			bottom: 18px;
			z-index: 10;
			height: 24px;
			line-height: 24px;
			padding: 0 12px;
			box-sizing: boder-box;
			font-size: 12px;
			border-radius: 12px;
			font-size: 10px;
			color: #fff;
			background: rgb(0,160,220);
			transition: all .2s;
		}
	}
	.info{
		padding: 18px;
		.title{
			line-height: 14px;
			margin-bottom: 6px;
			font-size: 14px;
			color: rgb(7,17,27)
		}
		.text{
			line-height: 24px;
			padding: 0 8px;
			font-size: 12px;
			color: rgb(77,85,93);
		}
	}
	.move-enter-active,.move-leave{
		transform: translate3d(0,0,0)
	}
	.move-enter,.move-leave-active{
		transform: translate3d(100%,0,0)
	}
	.fade-enter-active,.fade-leave{
		opacity: 1;
	}
	.fade-enter,.fade-leave-active{
		opacity: 0;
	}
</style>