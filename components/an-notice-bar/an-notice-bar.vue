<template>
	<view>
		<view class="an-notice-box" :style="'background-color: '+bgColor+';'">
			<view class="an-notice-icon">
				<uni-icons
				  :color="color"
				  type="sound"
				  size="14" />
			</view>
			<view class="an-notice-content">
				<view v-for="(text, index) in list" :key="index" v-if="number == index" class="an-notice-content-item" :style="'animation: anotice '+switchTime+'s linear;'">
					<text class="an-notice-content-item-text" :style="'color: '+color+';'">{{showSerial?index+1+'. ':''}}{{text}}</text>
				</view>
			</view>
			<view class="an-notice-more" @click="more">
				<text>查看更多</text>
				<uni-icons type="arrowright" color="#999" size="12" />
			</view>
		</view>
	</view>
</template>

<script>
	import uniIcons from '@/components/uni-icon/uni-icon.vue'
	export default {
		components: {
			uniIcons
		},
		props:{
			text: {
				type: "",
				default: '暂无消息'
			}, 
			color: {
				type: String,
				default: '#de8c17'
			},
			bgColor: {
				type: String,
				default: '#fffbe8'
			},
			switchTime: {
				type: Number,
				default: 5
			},
			showSerial: {
				type: Boolean,
				default: true
			}
		},
		data() {
			return {
				number: 0,
				list: []
			};
		},
		created() {
			this.list = this.text.split('|');
			this.startMove();
		},
		methods: {			
			startMove () {
			  // eslint-disable-next-line
			  let timer = setTimeout(() => {
				if (this.number === this.list.length-1) {
				  this.number = 0;
				} else {
				  this.number += 1;
				}
				this.startMove();
			  }, this.switchTime*1000);
			},
			more(){
				this.$emit('more')
			}
		}
	}
</script>

<style>
	.an-notice-box{
		width: 100%; 
		height: 60upx; 
		padding: 0 10upx; 
		overflow: hidden; 
		margin: 20upx 0; 
		display: flex; 
		justify-content: flex-start;
	}
	.an-notice-icon{
		width: 60upx; 
		height: 60upx; 
		line-height: 50upx; 
		text-align: center; 
		position: relative;
	}
	.an-notice-content{
		width: calc(100% - 220upx); 
		position: relative; 
		font-size: 14px;
	}
	.an-notice-content-item{
		width: 100%; 
		height: 60upx; 
		text-align: left; 
		line-height: 60upx;
	}
	.an-notice-content-item-text{
		display: block; 
		white-space: nowrap; 
		text-overflow: ellipsis; 
		overflow: hidden;
	}
	.an-notice-more{
		width: 130upx; 
		height: 60upx; 
		font-size: 12px; 
		line-height: 60upx; 
		text-align: right; 
		color: #999;
	}
	
	@keyframes anotice {
		 0%  {transform: translateY(80%);}
	    30%  {transform: translateY(0);}
	    70%  {transform: translateY(0);}
	   100%  {transform: translateY(-100%);}
	}
</style>
