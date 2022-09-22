<template>
	<view class="step_box">
		<view v-for="(item,index) in list" class="step_item">
			<text class="item_icon"></text>
			<view class="descBox">
			<text class="desc">{{item.desc}}</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name: 'steps',
		props: {
		list: {
			type: Array,//定义传值类型
			default: function() {
				return {}
			}

		}
},
		watch: {
					list(newValue, oldValue) {
						console.log('num新值：', newValue, 'num旧值', oldValue)
					},
		},
		data() {
			return {
				// list: [{ title: 'XX公司一', desc: '负责官网，小程序，系统的开发', date: '2018-11-11' },
				// 	{ title: 'XX公司二', desc: '负责官网，小程序，系统的开发', date: '2018-11-11' },
				// 	{ title: 'XX公司三', desc: '负责官网，小程序，系统的开发', date: '2018-11-11' },
				// 	{ title: 'XX公司四', desc: '负责官网，小程序，系统的开发', date: '2018-11-11' }
				// ]
			}
		}
	}
</script>

<style>
	.step_box {
		padding:0 60rpx;
	}

	.step_item {
		border-left: dotted 1px #675620;
		padding: 20rpx 60rpx;
		display: flex;
		flex-direction: column;
		position: relative;
		text-align:left;
	}
	.item_icon{
			position: absolute;
			width:30rpx;
			height: 30rpx;
			display:block;
			top:60rpx;
			left:-20rpx;
			background-color:#675620 ;
			 border-radius: 50%;
	}
	.descBox{
		background-color: #675620;
		color: #fff;
		padding: 30rpx 30rpx;
		border-radius: 30rpx;
	}
	.desc{
		font-size: 24rpx;
	}
</style>
