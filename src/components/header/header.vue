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
    <transition name="fade">
      <div v-show="detailShow" class="detail">
        <div class="detail-wrapper clearfix">
          <div class="detail-main">
            <h1 class="name">{{seller.name}}</h1>
            <div class="star-wrapper">
              <star :size="48" :score="seller.score"></star>
            </div>
            <div class="title">
              <div class="line"></div>
              <div class="text">优惠信息</div>
              <div class="line"></div>
            </div>
            <ul v-if="seller.supports" class="supports">
              <li class="support-item" v-for="item in seller.supports">
                <span class="icon" :class="classMap[item.type]"></span>
                <span class="text">{{item.description}}</span>
              </li>
            </ul>
            <div class="title">
              <div class="line"></div>
              <div class="text">商家通告</div>
              <div class="line"></div>
            </div>
            <div class="bulletin">
              <p class="content">{{seller.bulletin}}</p>
            </div>
          </div>
        </div>
        <div class="detail-close" @click="hideDetail">
          <i class="icon-close"></i>
        </div>
      </div>
    </transition>
  </div>
</template>

<script type="text/ecmascript-6">
import star from '@/components/star/star.vue';

  export default{
  	props: {
  		seller: {
  			type: Object
  		}
  	},
  	data() {
  		return {
  			detailShow: false
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
      position: relative;
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
					font-size: 10px;
					color: #fff;
					margin-left:2px;
					font-size: 10px;
					line-height: 24px;
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
				vertical-align:top;
				width: 10px;
				height:10px;
				font-size: 10px;
				color: #fff;
				line-height: 10px;
				position: absolute;
				top: 9px;
				right: 12px;
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
			transition:all linear .5s;
	        background: rgba(7,17,27,0.8);
	        backdrop-filter:blur(10px);
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
          .star-wrapper{
            margin-top: 18px;
            padding: 2px 0;
            text-align: center;
          }
          .title{
            display: flex;
            width: 80%;
            margin: 28px auto 24px auto;
            .line{
              flex:1;
              position: relative;
              top:-6px;
              border-bottom: 1px solid rgba(255,255,255,0.2);
            }
            .text{
              padding: 0 12px;
              font-weight:700;
              font-size:14px;
            }
          }
          .supports{
            width: 80%;
            margin: 0 auto;
            .support-item{
              padding: 0 12px;
              margin-bottom: 12px;
              font-size:0;
              &:last-child{
                margin-bottom: 0;
               }
               .icon{
                 display: inline-block;
                 width: 16px;
                 height: 16px;
                 vertical-align: top;
                 margin-right:6px;
                 background-size:16px 16px;
                 background-repeat:no-repeat;
                  &.decrease{
                   @include bg-image('decrease_2');
                   }
                  &.discount{
                   @include bg-image('discount_2');
                   }
                  &.guarantee{
                   @include bg-image('guarantee_2');
                   }
                  &.invoice{
                   @include bg-image('invoice_2');
                   }
                  &.special{
                   @include bg-image('special_2');
                   }
               }
              .text{
                /*height: 16px;*/
                line-height:16px;
                font-size:12px;
              }
            }

          }
          .bulletin{
            width: 80%;
            margin: 0 auto;
            .content{
              padding:0 12px;
              line-height:24px;
              font-size:12px;
            }
          }
				}
			}
			.detail-close{
				position: relative;
				width: 32px;
				height: 32px;
				margin: -64px auto 0 auto;
				clear: both;
				.icon-close{
					display:inline-block;
					text-align:center;
					line-height:32px;
					font-size: 32px;
					color: rgba(255,255,255,0.5);
				}
			}
		}
	}
.fade-enter-active,.fade-leave{
  opacity: 1;
}
.fade-enter,.fade-leave-active{
  opacity: 0;
}
</style>
