<template>
	<view class="content">
		<view>
			<image src="../../static/logo_chield.png" style="width: 100%;"></image>
		</view>
		<view>
			<button type="default" @click="goto('anLayer')">AnLayer</button>
		</view>
		<view>
			<button type="default" @click="goto('anTextAreaTip')">AnTextAreaTip</button>
		</view>
		<view>
			<button type="default" @click="goto('anImage')">AnImage</button>
		</view>
		<view>
			<an-notice-bar :text="noticeMsg" @more="more"></an-notice-bar>
		</view>
	</view>
</template>

<script>
	import AnNoticeBar from '../../components/an-notice-bar/an-notice-bar.vue'
	export default {
		components: {
			AnNoticeBar
		},
		data() {
			return {
				servicePages: {
					anLayer: '../an-layer/an-layer',
					anTextAreaTip: '../anTextAreaTip/anTextAreaTip',
					anImage: '../an-image/an-image',
				},
				noticeMsg: 'Hello Lucas|Hello Andot | andot.org Andot Studio'
			}
		},
		onLoad() {

		},
		methods: {
			goto(type){
				uni.navigateTo({
					url: this.servicePages[type]
				})
			},
			more(){
				uni.showToast({
					title: '查看更多'
				})
			}
		}
	}
</script>

<style>
	.content {
		text-align: center;
		height: 400upx;
	}

	.logo {
		height: 200upx;
		width: 200upx;
		margin-top: 200upx;
	}

	.title {
		font-size: 36upx;
		color: #8f8f94;
	}
	
	button{
		margin: 10upx;
	}
</style>
