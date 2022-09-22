<template>
	<view class="container" catchtouchmove='true'>
		<block v-for="(item,index) in chatList" :key="index">
			<view class="chat-one leftMsg" v-if="!item.isMe">
				<image class="chat-face" src="@/static/imgs/face1.jpg"></image>
				<view class="chat-box">
					<!-- <view class="chat-sender">知心姐姐</view> -->
					<view v-if="item.type=== 'txt'">{{item.content}}</view>
					<image v-if="item.type=== 'img'" :src="item.content" mode="widthFix"></image>
				</view>
			</view>
			<view v-else class="chat-one rightMsg chat-one-mine">
				<view class="chat-box">
					<image v-if="item.type=== 'img'" :src="item.content" mode="widthFix"></image>
					<view v-if="item.type=== 'txt'">{{item.content}}</view>
				</view>
				<image class="chat-face" src="@/static/imgs/face2.jpg"></image>
			</view>

		</block>
		<view class="chatbox-bottom">
			<input class="m-input" type="text" placeholder="请输入聊天内容" v-model="myInput" confirm-type="search" @confirm="sendMsg"
				cursor-spacing="16" />
			<image class="img-chose" src="@/static/imgs/img.png" @click="choseImgAndSend"></image>
			<button @click="sendMsg" class="btnEnter">发送</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				// 保存聊天的内容
				chatList: [{
						isMe: false,
						type: 'txt',
						content: '你好，我是可爱的知心姐姐，请问你想和我聊什么呢？'
					}, {
						isMe: false,
						type: 'img',
						content: '/static/imgs/1.jpg'
					},
					{
						isMe: true,
						type: 'txt',
						content: '你真漂亮！'
					},
					{
						isMe: true,
						type: 'img',
						content: '/static/imgs/2.jpg'
					}
				],
				myInput: ''
			}
		},
		onShow() {
			if (!!uni.getStorageSync('chatList')) {
				this.chatList = JSON.parse(uni.getStorageSync('chatList'))
				uni.pageScrollTo({
					duration: 0,
					scrollTop: 9999999999 //滚动高度，单位px，这里也可用选择器属性:selector:选择器
				})
			}
		},
		methods: {
			sendMsg() {
				if (!this.myInput) return
				let senMsg = {
					isMe: true,
					type: 'txt',
					content: this.myInput
				}
				this.chatList.push(senMsg)
				let renMsg = {
					isMe: false,
					type: 'txt',
					content: this.myInput
				}
				this.chatList.push(renMsg)
				uni.setStorageSync('chatList', JSON.stringify(this.chatList))
				this.myInput = ''
			},
			choseImgAndSend() {
				uni.chooseImage({
					count: 1,
					sizeType: ['original', 'compressed'],
					sourceType: ['album', 'camera'],
					success: res => {
						console.log(res.tempFilePaths[0])
						let senMsg = {
							isMe: true,
							type: 'img',
							content: res.tempFilePaths[0]
						}
						this.chatList.push(senMsg)
						let renMsg = {
							isMe: false,
							type: 'img',
							content: res.tempFilePaths[0]
						}
						this.chatList.push(renMsg)

						uni.pageScrollTo({
							duration: 0,
							scrollTop: 9999999999 //滚动高度，单位px，这里也可用选择器属性:selector:选择器
						})
						uni.setStorageSync('chatList', JSON.stringify(this.chatList))


					}
				})
			}
		}
	}
</script>

<style lang="scss">
	.container {
		height: 100%;

		.chat-one {
			display: flex;
			padding: 10px;
			justify-content: flex-start;

			.chat-face {
				width: 30px;
				height: 30px;
				border-radius: 50%;
			}

			.chat-box {
				padding: 5px;

				image {
					width: 300rpx;
					height: 200rpx;
				}
			}

			padding-bottom: 80px;
		}

		.rightMsg {
			justify-content: flex-end;
		}

		.chatbox-bottom {
			position: fixed;
			height: 88rpx;
			bottom: 0;
			border: solid 1px #f1f1f1;
			background-color: #fff;
			width: 100%;
			display: flex;
			justify-content: space-between;
			align-items: center;
			padding: 10rpx 20rpx;

			.m-input {
				color: #000;
				flex: 3;
				// border: solid 1px #f00;
				height: 80rpx;
				padding: 0 10rpx;
			}

			.img-chose {
				width: 30px;
				height: 30px;
				// flex: 1;
				margin: 0 4px;
			}

			.btnEnter {
				width: 120px;
				background-color: #4e9646;
				color: #fff;
				height: 80rpx;
				line-height: 80rpx;
				font-size: 32rpxß;
				margin-left: 10rpx;
				margin: 0 30rpx;
			}
		}

	}
</style>
