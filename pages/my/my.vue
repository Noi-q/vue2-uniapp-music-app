<template>
	<view class="my">
		<view class="top">
			
			<view class="author">
				<view class="author-name">
					<view class="logo">
						<image src="https://avatars.githubusercontent.com/u/76736117?v=4" mode="scaleToFill"></image>
					</view>
					<view class="app">
						<i class="icofont-technorati">  版本: 1.0.8</i>
						<br>
						<i class="icofont-user-alt-7">  作者: Noi-q</i>
					</view>
				</view>
			</view>
			
			<view class="set">
				<view class="set-list">
					<view class="list-like">
						<view class="icon">
							<i class="icofont-ui-love icofont-2x"></i>
						</view>
						<text>我的喜欢</text>
					</view>
					<view class="list-like">
						<view class="icon">
							<i class="icofont-download icofont-2x"></i>
						</view>
						<text>下载管理</text>
					</view>
					<view class="list-like">
						<view class="icon">
							<i class="icofont-music-alt icofont-2x"></i>
						</view>
						<text>我的歌单</text>
					</view>
					<view class="list-like">
						<view class="icon">
							<i class="icofont-headphone icofont-2x"></i>
						</view>
						<text>听歌记录</text>
					</view>
				</view>
			</view>
			
			<view class="set">
				<view class="set-list">
					<view class="list-like">
						<view class="icon" @click="fankui">
							<i class="icofont-question icofont-2x"></i>
						</view>
						<text>问题反馈</text>
					</view>
					<view class="list-like">
						<view class="icon" @click="Money">
							<i class="icofont-love icofont-2x"></i>
						</view>
						<text>赞助打赏</text>
					</view>
					<view class="list-like">
						<view class="icon" @click="Update">
							<i class="icofont-arrow-up icofont-2x"></i>
						</view>
						<text>检查更新</text>
					</view>
					<view class="list-like">
						<view class="icon" @click="GetURL">
							<i class="icofont-imac icofont-2x"></i>
						</view>
						<text>开源官网</text>
					</view>
				</view>
			</view>
			
			<view class="footer">
				<view class="xiaohua">
					<text>{{xiaohua}}</text>
				</view>
				<br><br>
				<view style="text-align: center;">Noi-q : '如果生活不如意,请记住还有我hgy'</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				xiaohua:''
			}
		},
		onLoad() {
			uni.request({
				url:'https://api.muxiaoguo.cn/api/yiyan?api_key=a2e41a76ea7ccc63',
				success: res => {
					// console.log(res.data.data.title)
					this.xiaohua = res.data.data.content
				}
			})
		},
		methods: {
			GetURL(){
				uni.showModal({
					title:'开源官网',
					content:'https://github.com/Noi-q/music-app',
					showCancel:false,
					// editable:true
				})
			},
			Money(){
				uni.showModal({
					// title:'开源官网',
					content:'感谢，但是暂时不缺钱',
					showCancel:false,
					// editable:true
				})
			},
			Update(){
				uni.showModal({
					// title:'开源官网',
					content:'请去Github查看更新',
					showCancel:false,
					// editable:true
				})
			},
			fankui(){
				uni.showModal({
					// title:'开源官网',
					content:'请加QQ:1044550927',
					showCancel:false,
					// editable:true
				})
			}
		}
	}
</script>

<style lang="less" scoped>
	@import url("./fonts/icofont.css");
	.my{
		.top{
			.author{
				background-color: #33302f;
				height: 250rpx;
				
				// width: 250rpx;
				margin: 20rpx;
				border-radius: 20rpx;
				.author-name{
					// background-color: red;
					height: 250rpx;
					display: flex;
					flex-direction: row;
					.logo{
						display: flex;
						flex-direction: column;
						justify-content: center;
						height: 250rpx;
						width: 40%;
						// background-color: red
						image{
							// background-color: red;
							width: 200rpx;
							height: 200rpx;
							border-radius: 20rpx;
							box-shadow: 0 0 5px black;
							margin-left: 30rpx;
						}
					}
					.app{
						// background-color: skyblue;
						height: 250rpx;
						width: 60%;
						display: flex;
						flex-direction: column;
						justify-content: center;
						i{
							color: white;
						}
					}
				}

			}
			
			.set{
				margin-top: 30rpx;
				.set-list{
					// background-color: skyblue;
					height: 210rpx;
					margin: 20rpx;
					border-radius: 20rpx;
					display: flex;
					flex-direction: row;
					// justify-content: center;
					box-shadow: 0 0 10px #d6d3d3;
					.list-like{
						// background-color: red;
						display: flex;
						flex-direction: column;
						height: 200rpx;
						width: 25%;
						text-align: center;
						.icon{
							// background-color: red;
							display: flex;
							flex-direction: row;
							justify-content: center;
							padding: 20rpx;
							padding-bottom: 50rpx;
							// font-size: 20rpx;
							i{
								color: #76cd76;
								// border: 1px solid #76cd76;
							}
						}
					}
				}
			}
			
			.footer{
				.xiaohua{
					text-align: center;
					word-wrap: break-word;
				}
			}
		}
	}
</style>
