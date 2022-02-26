<template>
	<view class="like">
		<view class="top">
			<i class="icofont-reply icofont-2x font-css" @click="back"></i>
			<view>
				<text>我的喜欢</text>
			</view>
		</view>
		<view class="center">
			
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			back(){
				uni.switchTab({
					url:'../music_circle/music_circle'
				})
			}
		}
	}
</script>

<style lang="less" scoped>
	@import url("./fonts/icofont.css");
	
	.like{
		.top{
			display: flex;
			flex-direction: row;
			.font-css{
				margin: 40rpx;
			}
			view{
				// background-color: red;
				text-align: center;
				// margin: 40rpx
				
				align-self: center;
				// text-align: center;
				text{
					font-size: 30rpx;
				}
			}
		}
	}
</style>
