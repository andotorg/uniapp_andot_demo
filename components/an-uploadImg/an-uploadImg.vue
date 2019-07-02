<template>
	<view>
		<view class="an-uploadImg-group">
			<view>
				<view class="an-img" v-for="(item, index) in imgList" :key="index" @click="perviewImg(index)">
					<image :src="item" v-if="item"></image>
					<view class="an-icon-close" @click.stop="handleRemove(index)">
						<uni-icon type="closeempty" size="26" color="#F00"></uni-icon>
					</view>
				</view>
				<view class="an-img-add" @click="chooseImage">
					<uni-icon type="plus" size="36" color="#FFFFFF"></uni-icon>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import uniIcon from '@/components/uni-icon/uni-icon.vue'
	
	export default {
		name: 'AnUploadImg',
		components:{
			uniIcon
		},
		data() {
			return {
				imgList: [],
				imgBase64List: []
			};
		},
		methods:{
			chooseImage() {
				uni.chooseImage({
				  success: (chooseImageRes) => {
					for (var i = 0; i < chooseImageRes.tempFilePaths.length; i++) {
						this.imgList.push(chooseImageRes.tempFilePaths[i]);
						uni.getFileSystemManager().readFile({
							filePath: chooseImageRes.tempFilePaths[i], //选择图片返回的相对路径
							encoding: 'base64', //编码格式
							success: res => { //成功的回调
								let base64 = 'data:image/jpeg;base64,' + res.data //不加上这串字符，在页面无法显示的哦
								this.imgBase64List.push(base64);
							}
						})
					}
				  }
				})
			},
			perviewImg(index){
				let urls = [];
				if(index != -1){
					urls[0] = this.imgList[index];
				}else{
					urls = this.imgList;
				}
				uni.previewImage({
					urls: urls
				});
			},
			handleRemove(index){
				
			}
		}
	}
</script>

<style>
	.an-uploadImg-group{
		margin: 5upx 20upx;
	}
	.an-img{
		float: left; 
		margin-right: 10upx;
	}
	.an-img-add{
		float: left; 
		margin-right: 10upx; 
		height: 100upx; 
		width: 100upx; 
		background-color: #C8C7CC; 
		text-align: center; 
		line-height: 110upx;
	}
	.an-img>image{
		height: 100upx; 
		width: 100upx;
	}
	.an-icon-close{
		position: relative; 
		right: -50upx; 
		top: -120upx;
	}
</style>
