<template>
	<view class="search">
		<view class="top">
			<i class="icofont-reply icofont-2x font-css" @click="back"></i>
			<input class="input" type="text" v-model="name" placeholder="搜索歌曲" />
			<view class="search-btn" @click="Search">
				<text>搜索</text>
			</view>
		</view>
		<view class="content">
			<view 
			class="search-music" 
			v-for="(sm,index) in SearchMusicList" 
			:key="index"
			@click="GetPlayer(sm.songid)"
			>
				<view class="music-num">
					<view class="num">
						<text>{{index+1}}</text>
					</view>
					<view class="music-name">
						<view>{{sm.name}}</view>
						<view>{{sm.author}}</view>
					</view>
					<view class="music-icon">
						<i class="icofont-gear icofont-1x"></i>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				name:'',
				SearchMusicList:[]
			}
		},
		onLoad() {
			uni.request({
				url:'http://api.guaqb.cn/music/music',
				method:'GET',
				data:{
					input:'热门歌曲',
					filter:'name',
					type:'163'
				},
				success:(res)=>{
					this.SearchMusicList = res.data.data
					// console.log(res.data.data)
				}
			})
		},
		methods: {
			back(){
				uni.switchTab({
					url:'../music_circle/music_circle'
				})
			},
			Search(){
				if(!this.name){
					return uni.showModal({
						title:'提示',
						content:'内容不能为空!',
						
					})
				}
				uni.request({
					url:'http://api.guaqb.cn/music/music',
					method:'GET',
					data:{
						input:this.name,
						filter:'name',
						type:'163'
					},
					success:(res)=>{
						this.SearchMusicList = res.data.data
						// console.log(res.data.data)
					}
				})
			},
			GetPlayer(songid){
				uni.navigateTo({
					url:`../player/player?songid=${songid}`
				})
			}
		}
	}
</script>

<style lang="less" scoped>
	@import url("./fonts/icofont.css");
	.search{
		.top{
			background-color: white;
			display: flex;
			flex-direction: row;
			position: sticky;
			top: 0;
			.font-css{
				margin: 40rpx;
				// background-color: red;
			}
			.input{
				// border: .5px solid gray;
				background-color: whitesmoke;
				border-radius: 50px;
				margin: 30rpx;
				padding: 20rpx;
				// width: 200rpx;
			}
			.search-btn{
				margin: 30rpx;
				background-color: #434343;
				border-radius: 50px;
				width: 200rpx;
				height: 80rpx;
				text-align: center;
				display: flex;
				flex-direction: column;
				justify-content: center;
				// padding: 20rpx;
				text{
					color: white;
				}
			}
		}
		.content{
			.search-music:hover{
				background-color: whitesmoke;
			}
			.search-music{
				// background-color: red;
				.music-num{
					display: inline-block;
					padding: 20rpx;
					// background-color: skyblue;
					display: flex;
					flex-direction: row;
					// justify-content: center;
					.num{
						display: flex;
						flex-direction: column;
						justify-content: center;
						// background-color: red;
						text{
							flex-grow: 1;
							padding: 20rpx;
						}
					}
					.music-name{
						display: inline-block;
						// background-color: yellow;
						// padding: 20rpx;
					}
					.music-name{
						flex-grow: 5;
					}
					.music-icon{
						// flex-grow: 3;
						display: flex;
						flex-direction: column;
						justify-content: center;
					}
					
				}

			}
		}
	}
</style>
