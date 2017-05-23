<template>
  <div class="header">
    <div class="content-wrapper">
    	<div class="avatar">
    		<img width="64" height="64" :src="seller.avatar" alt="">
    	</div>
    	<div class="content">
    		<div class="title">
    			<span class="brand"></span>
    			<span class="name">{{seller.name}}</span>
    		</div>
    		<div class="description">
    			{{seller.description}}/{{seller.deliveryTime}}分钟送达
    		</div>
    		<div v-if="seller.supports" class="support">
    			<span class="icon" :class="classMap[seller.supports[0].type]"></span>
    			<span class="text">{{seller.supports[0].description}}</span>
    		</div>
    	</div>
    	<div v-if="seller.supports" class="support-count" @click="showDetail">
    		<span class="count">{{seller.supports.length}}个</span>
    		<i class="icon-keyboard_arrow_right"></i>
    	</div>
    </div>
    <div class="bullentin-wrapper" @click="showDetail">
    	<span class="bulletin-title"></span>
    	<span class="bulletin-text">{{seller.bulletin}}</span>
    	<i class="icon-keyboard_arrow_right"></i>
    </div>
    <div class="background">
    	<img :src="seller.avatar" width="100%" height="100%">
    </div>
    <div v-show="detailShow" class="detail">
    	<div class="detail-wrapper clearfix">
    		<div class="detail-main">
    			<h1 class="name">{{seller.name}}</h1>
    			<star :size="48" :score="seller.score"></star>
    		</div>
    	</div>	
    	<div class="detail-close" @click="hideDetail">
    		<i class="icon-close"></i>
    	</div>
    </div>
  </div>
</template>

<script>
import star from '@/components/star/star.vue';

  export default{
  	props: {
  		seller: {
  			type: Object
  		}
  	},
  	data() {
  		return {
  			detailShow: true
  		}
  	},
  	methods:{
  		showDetail() {
  			this.detailShow = true;
  		},
  		hideDetail() {
  			this.detailShow = false;
  		}
  	},
  	created() {
  		this.classMap = ['decrease','discount','special','invoice','guarantee']
  	},
  	components:{
  		star
  	}
  }
 
</script>

<style lang="scss" scoped>
@import "../../common/css/mixin";
	.header{
		overflow:hidden;
		color:#fff;
		background:rgba(7,17,27,0.5);
		position:relative;
		.content-wrapper{
			padding:24px 12px 18px 24px;
			font-size: 0;
			position:relative;
			.avatar{
				display:inline-block;
				vertical-align:top;
				img{
					border-radius: 2px;
				}
			}
			.content{
				display:inline-block;
				vertical-align: top;
				margin-left:16px;
				font-size:14px;
				.title{
					margin: 2px 0 8px 0;
					.brand{
						display: inline-block;
						vertical-align: top;
						width: 30px;
						height: 18px;
						@include bg-image('brand');
						background-size: 30px 18px;
						background-repeat: no-repeat;
					}
					.name{
						margin-left: 6px;
						font-size: 16px;
						line-height: 18px;
						font-weight: bold;
					}
				}
				.description{
					margin-bottom: 10px;
					line-height: 12px;
					font-size: 12px;
				}
				.support{
					.icon{
						display: inline-block;
						width: 12px;
						height: 12px;
						vertical-align:top;
						margin-right: 4px;
						background-size: 12px 12px;
						background-repeat: no-repeat;
						&.decrease{
							@include bg-image('decrease_1');
						}
						&.discount{
							@include bg-image('discount_1');
						}
						&.guarantee{
							@include bg-image('guarantee_1');
						}
						&.invoice{
							@include bg-image('invoice_1');
						}
						&.special{
							@include bg-image('special_1');
						}
					}
					.text{
						display: inline-block;
						vertical-align: top;
						line-height: 12px;
						font-size:10px;
					}
				}
			}
			.support-count{
				position:absolute;
				right: 12px;
				bottom: 18px;
				padding: 0 8px;
				height: 24px;
				line-height: 24px;
				border-radius: 14px;
				background: rgba(0,0,0,0.2);
				text-align:center;
				.count{
					vertical-align:top;
					font-size: 10px;
				}
				.icon-keyboard_arrow_right{
					display:inline-block;
					vertical-align:top;
					width: 10px;
					height:10px;
					background:url('./keyboard_arrow_right.svg') no-repeat;
					background-size:10px 10px;
					margin:7px 0 0 2px;
					// margin-left:2px;
					// font-size: 10px;
					// line-height: 24px;
				}
			}
		}
		.bullentin-wrapper{
			height: 28px;
			background: rgba(7,17,27,0.2);
			line-height: 28px;
			padding: 0 22px 0 12px;
			white-space: nowrap;
			overflow: hidden;
			text-overflow: ellipsis;
			font-size: 0;
			position: relative;
			.icon-keyboard_arrow_right{
				display:inline-block;
				// vertical-align:top;
				width: 10px;
				height:10px;
				background:url('./keyboard_arrow_right.svg') no-repeat;
				background-size:10px 10px;
				position: absolute;
				top: 9px;
				right: 12px;
				// margin:9px 12px 0 0;
			}
			.bulletin-title{
				display: inline-block;
				vertical-align:middle;
				width: 22px;
				height: 12px;
				@include bg-image('bulletin');
				background-size: 22px 12px;
				background-repeat: no-repeat;
			}
			.bulletin-text{
				vertical-align: middle;
				font-size: 10px;
				margin: 0 4px;
			}
		}
		.background{
			position:absolute;
			left: 0;
			top: 0;
			width: 100%;
			height: 100%;
			z-index: -1;
			filter:blur(10px);
		}
		.detail{
			position: fixed;
			top:0;
			left:0;
			z-index: 100;
			width: 100%;
			height: 100%;
			overflow: auto;
			background: rgba(7,17,27,0.8);
			.detail-wrapper{
				min-height: 100%;
				width: 100%;
				// position:relative;
				.detail-main{
					margin-top: 64px;
					padding-bottom: 64px; 
					.name{
						line-height: 16px;
						text-align: center;
						font-size: 16px;
						font-weight: 700;
					}
				}
			}
			.detail-close{
				position: relative;
				width: 32px;
				height: 32px;
				margin: -64px auto 0 auto;
				cursor:pointer;
				clear: both;
				.icon-close{
					display:inline-block;
					vertical-align:bottom;
					width:28px;
					height:3px;
					background:rgba(255,255,255,0.5);
					transform: rotate(45deg);
					position:relative;
				}
				.icon-close:before{
					content: '';
					display: inline-block;
					width: 28px;
					height: 3px;
					background:rgba(255,255,255,0.5);
					position: absolute;
					left:0;
					top:0;
					transform: rotate(90deg);
				}
			}
		}
	}
</style>
