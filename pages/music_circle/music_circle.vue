<template>
	<view class="Top-music">
		<!-- 顶部tabbar -->
		<view class="Top">
			<view v-for="item in list" :key="item.id">
				<view class="Home clear" v-if="(item.type == 1)" @click="select(item)">
					<text>{{item.title}}</text>
				</view>
				<view class="Home unclear" v-if="(item.type != 1)" @click="select(item)">
					<text>{{item.title}}</text>
				</view>
			</view>
		</view>
		<scroll-view scroll-y="true" class="content" v-for="item in list" :key="item.id">
			<!-- 轮播图 -->
			<view class="map" v-if="(item.type == 1 && item.id == 0)">
				
				<view class="">
					<swiper class="swiper" :indicator-dots="true" :autoplay="true" :interval="3000" :duration="500">
						<swiper-item class="swiper-item" v-for="img in SwiperList" :key="img.id">
							<image :src="img.url" mode="aspectFit"></image>
						</swiper-item>
					</swiper>
				</view>
				
				<!-- 中间按钮 -->
				<view class="btns">
					<view class="btn-clear" @click="getDay">
						<view class="btn">
							<view class="icofont-list icofont-2x btn-color"></view>
						</view>
						<text>每日推荐</text>
					</view>
					<view class="btn-clear" @click="getLike">
						<view class="btn">
							<view class="icofont-heart icofont-2x btn-color"></view>
						</view>
						<text>我的喜欢</text>
					</view>
					<view class="btn-clear" @click="localMusic">
						<view class="btn">
							<view class="icofont-music icofont-2x btn-color"></view>
						</view>
						<text>本地音乐</text>
					</view>
					<view class="btn-clear" @click="getSearch">
						<view class="btn">
							<view class="icofont-search-2 icofont-2x btn-color"></view>
						</view>
						<text>音乐搜索</text>
					</view>
				</view>
				
				<!-- 热门歌曲 -->
				<view class="hotmusic">
					<view style="margin-left: 20rpx;">
						<i class="icofont-music-notes"></i>
						<text style="font-size: 30rpx;">热门歌曲</text>
					</view>
					<scroll-view class="music" scroll-x="true" @scroll="musicScroll">
						<view class="music-item" v-for="hotItem in hotMusicList" :key="hotItem.id" @click="PlayerHotMusic(hotItem.songid)">
							<image :src="hotItem.pic"></image>
							<view class="music-item-name">{{hotItem.name.slice(0,6)}}</view>
						</view>

					</scroll-view>
				</view>
				
				<!-- 最新歌单 -->
				<view class="hotmusic">
					<view style="margin-left: 20rpx;">
						<i class="icofont-music-disk"></i>
						<text style="font-size: 30rpx;">最新歌曲</text>
					</view>
					<scroll-view class="music" scroll-x="true" @scroll="musicScroll">
						<view class="music-item" v-for="newItem in newMusicList" :key="newItem.id" @click="PlayerNewMusic(newItem.songid)">
							<image :src="newItem.pic"></image>
							<view class="music-item-name">{{newItem.name.slice(0,6)}}</view>
						</view>
					</scroll-view>
				</view>
			</view>
			<view class="" v-if="(item.type == 1 && item.id == 1)">
				待开发中
			</view>
			<view class="" v-if="(item.type == 1 && item.id == 2)">
				待开发中
			</view>
			<view class="" v-if="(item.type == 1 && item.id == 3)">
				待开发中
			</view>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
				list:[
					{
						id:0,
						title:'推荐',
						type:1
					},
					{
						id:1,
						title:'榜单',
						type:0
					},
					{
						id:2,
						title:'歌单',
						type:0
					},
					{
						id:3,
						title:'艺人',
						type:0
					},
				],
				// ListType:1
				SwiperList:[
					{
						id:0,
						url: require('./img/1.jpg')
					},
					{
						id:1,
						url:require('./img/2.jpg')
					},
					{
						id:2,
						url: require('./img/3.jpg')
					}
				],
				hotMusicList:[],
				newMusicList:[]
			}
		},
		onLoad() {
			console.log(this.imgList)
			uni.request({
				url:'http://api.guaqb.cn/music/music',
				method:'GET',
				data:{
					input:'热门歌曲',
					filter:'name',
					type:'163'
				},
				success:(res)=>{
					this.hotMusicList = res.data.data
					// console.log(res.data.data)
				}
			})
			uni.request({
				url:'http://api.guaqb.cn/music/music',
				method:'GET',
				data:{
					input:'新歌曲',
					filter:'name',
					type:'163'
				},
				success:(res)=>{
					this.newMusicList = res.data.data
					// console.log(res.data.data)
				}
			})
		},
		methods: {
			musicScroll(e){
				// e.mp.preventDefault()
				// console.log(e)
				e.preventDefault()
				e.stopPropagation()
			},
			select(item){
				let _list = this.list
				if(item.type != 1){
					// console.log("true",item)
					item.type = 1
					// console.log(item)
					for(let i in _list){
						// console.log(_list[i])
						if(_list[i].id != item.id){
							_list[i].type = 0
						}
						// console.log(item)
					}
				}
			},
			
			// 每日推荐
			getDay(){
				uni.showModal({
					title:'',
					content:'待开发中...',
					showCancel:false
				})
			},
			
			// 本地音乐
			localMusic(){
				uni.showModal({
					title:'',
					content:'待开发中...',
					showCancel:false
				})
			},
			
			// 音乐搜索
			getSearch(){
				uni.navigateTo({
					url:'../search/search'
				})
			},
			// 我的喜欢
			getLike(){
				/*
				uni.navigateTo({
					url:'../mylike/mylike'
				})*/
				uni.showModal({
					title:'',
					content:'待开发中...',
					showCancel:false
				})
			},
			// 热门歌曲
			PlayerHotMusic(songid){
				console.log(songid)
				uni.navigateTo({
					url:`../player/player?songid=${songid}`,
				})
			},
			// 最新歌曲
			PlayerNewMusic(songid){
				uni.navigateTo({
					url:`../player/player?songid=${songid}`
				})
			}
		},
		// 下拉刷新
		onPullDownRefresh(){
			setTimeout(()=>{
				uni.stopPullDownRefresh()
			},2000)
		}
	}
</script>

<style scoped lang="less">
	@import url("./fonts/icofont.css");
	
	.Top-music{
		.Top{
			position: sticky;
			top: 0;
			background-color: white;
			color: white;
			height: 90rpx;
			// box-shadow: 0 0 5px gray;
			z-index: 1;
			display: flex;
			flex-direction: row;
			.clear{
				display: flex;
				flex-direction: column;
				margin: 5rpx 0 5rpx 5rpx;
				align-self: center;
				text{
					// display: inline-flex;
					// background-color: skyblue;
					color: #5cb85c;
					padding: 20rpx;
					align-self: center;
					font-size: 30rpx;
				}
			}
			.unclear{
				display: flex;
				flex-direction: column;
				margin: 5rpx 0 5rpx 5rpx;
				align-self: center;
				text{
					color: gray;
					padding: 20rpx;
					align-self: center;
					font-size: 30rpx;
				}
			}
		}
		.map{
			.swiper{
				width: 100%;
				height: 400rpx;
				// background-color: skyblue;
				.swiper-item{
					width: 100%;
					height: 400rpx;
					image{
						width: 100%;
						height: 400rpx;
						// background-color: red;
					}
				}
			}
			.btns{
				display: flex;
				flex-direction: row;
				justify-content: center;
				cursor: pointer;
				.btn-clear{
					text-align: center;
					.btn{
						margin: 20rpx;
						padding: 20rpx;
						text-align: center;
						background-color: #76cd76;
						border-radius: 10rpx;
						.btn-color{
							color: white;
						}
					}
					text{
						font-size:30rpx
					}
				}
			}
			.hotmusic{
				margin-top: 40rpx;
				// background-color: red;
				.music{
					// overflow: hidden;
					// background-color: skyblue;
					display: flex;
					flex-direction: row;
					white-space: nowrap;
					.music-item{
						// margin-top: 20rpx;
						margin: 30rpx 10rpx 20rpx 10rpx;
						display: inline-block;
						text-align: center;
						overflow: hidden;
						// background-color: red;
						cursor: pointer;
						image{
							width: 80px;
							height: 80px;
							border-radius: 10rpx;
						}
						.music-item-name{
							font-size: 28rpx;
							word-wrap: break-word;
							word-break: break-all;
							overflow: hidden;
						}
					}
				}
			}
		}
		.content{
			z-index: -1;
		}
	}
</style>
