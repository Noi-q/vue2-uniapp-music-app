<template>
	<view class="player">
		<view class="top">
			<view class="top-left" @click="Back">
				<view class="back">
					<i class="icofont-reply icofont-2x icon-size"></i>
					<text>返回</text>
				</view>
			</view>
		</view>
		<view class="center" v-for="m in music" :key="m.id">
			<image :src="m.pic" mode="heightFix"></image>
			<view style="margin-top:100rpx">
				<view>Music: {{m.name}}</view>
				<view>Author: {{m.author}}</view>
			</view>
			<view class="set">
				<view class="icon-color">
					<i  @click="like(m.songid)" class="icofont-ui-love icofont-2x i-clear"></i>
				</view>
			</view>
			<audio 
			:src="m.music" 
			:poster="m.pic" 
			:name="m.name" 
			:author="m.author" 
			controls
			style="margin-top: 50rpx;"
			></audio>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				music:[],
			}
		},
		methods: {
			Back(){
				uni.switchTab({
					url:'../music_circle/music_circle'
				})
			},
			like(id){
				// console.log(id)
				let _id = id
				/*
				uni.setStorage({
					key:'mylike',
					data:[
						_id
					],
					success:res=>{
						console.log(res)
						uni.showModal({
							content:'已加入我的喜欢',
							showCancel:false
						})
					},
					fail: err => {
						uni.showModal({
							content:'异常'
						})
					}
				})*/
				const value = uni.getStorageSync('mylike')
				if(!value.data){
					console.log(_id)
					return _id
				}else if(value.data){
					console.log(value.data + _id)
					return value.data + _id
				}
				uni.setStorageSync('mylike',[])
				console.log(uni.getStorageSync('mylike'))
			}
		},
		onLoad(e) {
			// console.log(e)
			if(!e.songid){
				uni.showModal({
					title:"提示",
					content:"没有找到该音乐"
				})
				uni.switchTab({
					url:'../music_circle/music_circle'
				})
			}
			uni.request({
				url:'http://api.guaqb.cn/music/music',
				method:'GET',
				data:{
					input:e.songid,
					filter:'id',
					type:'163'
				},
				success:(res)=>{
					this.music = res.data.data
					// console.log(res.data.data)
				}
			})
			
			/*
			// uni.createInnerAudioContext()
			const innerAudioContext = uni.createInnerAudioContext();
			innerAudioContext.autoplay = true;
			innerAudioContext.src = 'https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-hello-uniapp/2cc220e0-c27a-11ea-9dfb-6da8e309e0d8.mp3';
			innerAudioContext.onPlay(() => {
			  console.log('开始播放');
			});
			innerAudioContext.onError((res) => {
			  console.log(res.errMsg);
			  console.log(res.errCode);
			});
			*/
		}
	}
</script>

<style lang="less" scoped>
	@import url("./fonts/icofont.css");
	
	.player{
		.top{
			display: flex;
			flex-direction: row;
			.top-left{
				.back{
					// display: inline-block;
					padding: 20rpx;
					// background-color: skyblue;
					text{
						font-size: 35rpx;
					}
				}
			}
		}
		.center{
			margin-top: 80rpx;
			text-align: center;
			image{
				box-shadow: 0 0 5px gray;
				border-radius: 20rpx;
			}
			.icon-color{
				overflow: hidden;
				.i-clear{
					margin: 40rpx;
					float: left;
					color: gray;
				}
			}
		}
	}
</style>
