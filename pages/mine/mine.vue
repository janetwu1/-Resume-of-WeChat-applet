<template>
	<view class="container">
		<!-- 我的页面 -->
		<image
			src="https://janet-bucket.oss-cn-hangzhou.aliyuncs.com/wechat/resume_bg1.jpg?versionId=CAEQUhiBgMDJrM7RmhgiIGRlYThjODFmYmFkYzRmNTRhODc1MzAxYTU1NGNjYTA4"
			class="page_bg"></image>
		<view :style="{ position: 'absolute',width:'100%',height:'100%', left:0,top:statusLineHeight+'px'}">
			<view class="uni-margin-wrap swiper-father">
				<swiper class="swiper" circular :interval="interval" :duration="duration">
					<!--自我介绍-->
					<swiper-item>
						<view class="swiper-item uni-bg-red">
							<view class="mine_box personal_info">
								<text class="box-title">个人信息>></text>
								<view class="box-content">
									<text>姓名：吴平平</text>
									<text>前端经验：6年</text>
									<text>手机：{{mobile}}</text>
									<text>邮箱：{{email}}</text>
								</view>
							</view>
							<view class="mine_box">
								<text class="box-title">个人优势>></text>
								<view class="box-content">
									<text>1、有 6 年前端开发经验，有 2 年全栈开发经验，有 2 年后端经验。</text>
									<text> 2、能独立自主开发并部署项目。 </text>
									<text> 3、有良好的沟通能力和团队协作精神，能承受较大的工作压力。</text>
									<text>4、有强烈的责任心和较强的分析问题与解决问题的能力。 </text>
									<text>5、有一年左右带领前端团队的经验</text>
								</view>
							</view>
							<view class="mine_box">
								<text class="box-title">社交主页>></text>
								<view class="box-content">
									<text @click="copyMessage(csdn)">CSDN 博客：https://blog.csdn.net/janent168 </text>
									<text @click="copyMessage(github)">GitHub 网址：https://github.com/janetwu1</text>
								</view>
							</view>

						</view>
					</swiper-item>
					<!--技能展示-->
					<swiper-item>
						<view class="swiper-item uni-bg-green">
							<view class="pageMain">
								<text class="title_Left">技能展示</text>
								<skill :list="skillList"></skill>
							</view>
						</view>
					</swiper-item>
					<!--工作经验进度条-->
					<swiper-item>
						<view class="swiper-item uni-bg-green">
							<view class="pageMain">
								<text class="title_Left">工作经验</text>
								<steps :list="workExperience"></steps>
							</view>
						</view>
					</swiper-item>

					<!--项目经验-->
					<swiper-item>
						<view class="swiper-item uni-bg-green">
							<view class="pageMain">
								<text class="title_Left">项目经验</text>
								<steps :list="projectExperience"></steps>
							</view>
						</view>
					</swiper-item>
					<swiper-item>
						<view class="pageLast">
							<view class="box-content">
								<view class="myWechat">
									<image
										src='https://janet-bucket.oss-cn-hangzhou.aliyuncs.com/wechat/wechat.png?versionId=CAEQUhiBgID_lfSMmxgiIDVjYjY3NDUxYWI3NzRiMjJiYWY0Yjc0ZDAxZGU0NTFm'
										style="width:226rpx;height: 208rpx;"></image>
									<text class="font">个人微信</text>
								</view>
								<view class="myInfo"><text>姓名：吴平平</text>
									<text @click="getPhone">手机：{{mobile}}</text>
									<text @click="copyMessage(email)">邮箱：{{email}}</text>
									<a @click="getPhone" class="getPhone">
										<image src="@/static/images/mobile.png" class="image">
										</image>拨打电话
									</a>
									<a @click="copyMessage(email)" class="getPhone">
										<image src="@/static/images/email.png" class="image">
										</image>复制邮箱
									</a>
								</view>
							</view>
						</view>
					</swiper-item>
				</swiper>
			</view>
		</view>
	</view>
</template>

<script>
	import steps from '@/components/steps'
	import skill from '@/components/skill'
	export default {
		data() {
			return {
				mobile: '15201936528',
				email: 'janet168@126.com',
				csdn: 'https://blog.csdn.net/janent168',
				github: 'https://github.com/janetwu1',
				background: ['color1', 'color2', 'color3'],
				statusLineHeight: 0,
				indicatorDots: true,
				autoplay: true,
				interval: 2000,
				duration: 500,
				workExperience: [
					{ title: '上海人佩信息科技有限公司', desc: '负责官网，小程序，系统的开发，数据大屏以及threeJs的研究', date: '2021.3-2022' },
					{ title: '云康信息科技有限公司', desc: '负责官网，数据大屏，公众号h5页面，基因检测打印报告样式，以及其他领导步骤的内容', date: '2019.04-2020.12' },
					{ title: '望锋科技有限公司', desc: '负责pc官网，手机端h5的开发', date: '2017.04-2018.12' },
					{ title: '泽溪信息科技有限公司', desc: '负责官网，APP，oA系统的开发', date: '2016.04-2017.04' },
					{ title: '黄浦朝日进修学院', desc: '负责官网、SEO优化、其他校区网站页面的维护', date: '2013.03-2014.12' },
					{ title: '宝盒速递有限公司', desc: '负责官网，ERP系统的开发', date: '2012.03-2013.04' }
				],
				projectExperience: [
					{ title: '店装云', desc: '主要用于开店装修过程中的工程项目管理，子公司与客户之间的内外部协同，工人端（子公司工人用）（vue+elementUI）' },
					{ title: '门店H5端', desc: '维修维保品牌方可以通过手机链接或者扫码进入门店H5, 可以用手机就能查看维修的信息（uni-app）' },
					{ title: '维修维保管理系统（后台管理系统）', desc: ' 产品跟业务部门沟通了解维修维保的需求，带领整个前端团队完成整个项目的几个版本的迭代（vue+elementUI）' },
					{
						title: '智佩连锁餐饮加盟开店装修平台（小程序）',
						desc: '根据不同的角色选择（连锁品牌，品牌加盟商，装修公司，设计师和游客），每个角色能看到对应角色下的内容（原生小程序+Vant组件）'
					},
					{
						title: '智佩开店管家（小程序）',
						desc: ' 只有在获客小程序(智佩连锁餐饮加盟开店装修平台)中是品牌方的用户才能登录智佩开店管家小程序,用户可以在小程序上查看项目信息，上传付款凭证，查看监控等信息（原生小程序+Vant组件）'
					},
					{ title: '智佩官网', desc: '公司官网（https://www.matepei.com/）' }

				],
				skillList: [
					{ desc: '熟悉PS等设计类软件，熟练掌握 html、css并css3和html5 的新特性能快速精准还原设计图。 ' },
					{ desc: '熟悉原生小程序开发，能独立开发小程序' },
					{ desc: ' 熟悉 uni-app，vue，jquery 等主流框架' },
					{ desc: '熟悉echarts，highcharts可视化组件' },
					{ desc: '有常见前端框工具/库使用经验，如：webpack，Grunt，Gulp，UI组件等；' },
					{ desc: '熟悉 git 版本控制工具,了解SEO优化' }
				],
			}
		},
		components: { steps, skill },
		onLoad() {
			var _this = this
			uni.getSystemInfo({
				success: function(data) {
					console.log(data)
					console.log(data.statusBarHeight)
					_this.statusLineHeight = data.statusBarHeight *
						2 //获取状态栏高度 乘2是px与rpx转换 获取到的高度单位是px　　　
				}
			})
		},
		methods: {
			getPhone() {
				uni.makePhoneCall({
					phoneNumber: this.mobile, //电话号码
					success: function(e) {
						console.log(e)
					},
					fail: function(e) {
						console.log(e)

					}
				})
			},
			//复制
			copyMessage(value) {
				uni.setClipboardData({
					data: value,
					success: function(res) {
						uni.getClipboardData({
							success: function(res) {
								uni.showToast({ title: '复制成功', })
							},
						})
					},
				})
			},
			changeIndicatorDots(e) {
				this.indicatorDots = !this.indicatorDots
			},
			changeAutoplay(e) {
				this.autoplay = !this.autoplay
			},
			intervalChange(e) {
				this.interval = e.target.value
			},
			durationChange(e) {
				this.duration = e.target.value
			}
		}
	}
</script>

<style lang="scss">
	.container {
		height: 100vh;
		position: relative;
		color: #675620;

		.uni-margin-wrap {
			width: 100%;
			height: 100%;
		}

		.swiper {
			position: relative;
			height: 100vh;
		}

		.swiper-item {
			display: block;
			height: 100%;
			text-align: center;
			// border: solid 1px #f00;
			padding-top: 40rpx;
		}

		.swiper-list {
			margin-top: 40rpx;
			margin-bottom: 0;
		}

		.uni-common-mt {
			margin-top: 60rpx;
			position: relative;
		}

		.info {
			position: absolute;
			right: 20rpx;
		}

		.uni-padding-wrap {
			width: 550rpx;
			padding: 0 100rpx;
		}

		.page_bg {
			width: 100%;
			height: 100%;
			position: absolute;
			top: 0;
			left: 0;
			z-index: -1;
		}

		.mine_box {
			padding: 20rpx 80rpx;

			.box-title {
				font-size: 36rpx;
				width: 100%;
				border-bottom: dotted 1px #333;
				padding-bottom: 20rpx;
				display: block;
				text-align: left;
			}

			.box-content {
				display: flex;
				flex-direction: column;
				font-size: 28rpx;
				line-height: 2;
				padding: 20rpx 0;
				text-align: left;
			}
		}
		.pageMain {
			display: flex;
			.title_Left {
				background-color: #675620;
				// width: 50px;
				height: auto;
				color: #fff;
				display: block;
				writing-mode: tb-rl;
				padding: 20rpx 10rpx;
				height: 100px;
				margin-left: 30rpx;
				margin-top: 50px;
				border-radius: 30rpx;
				letter-spacing: 5px;
			}
		}
		.pageLast {
			padding: 20rpx 80rpx;
			.box-content {
				padding: 120rpx 0;
				display: flex;
				flex-direction: column;
				align-items: center;
				width: 100%;

				.myWechat {
					width: 100%;
					display: flex;
					flex-direction: column;
					justify-content: center;
					align-items: center;

					.font {
						font-size: 24rpx;
						height: 40rpx;
						line-height: 40rpx;
					}
				}

				.myInfo {
					display: flex;
					flex-direction: column;
					font-size: 28rpx;
					line-height: 2;
					width: 60%;
					margin-top: 40rpx;
				}

				.getPhone {
					height: 64rpx;
					font-size: 28rpx;
					border-radius: 32rpx;
					border: solid 1px #675620;
					display: flex;
					align-items: center;
					justify-content: center;
					margin-top: 20px;

					.image {
						width: 40rpx;
						height: 40rpx;
						margin-right: 5px;
					}
				}
			}
		}
	}
</style>
