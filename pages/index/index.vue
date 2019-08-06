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
	</view>
</template>

<script>
	export default {
		data() {
			return {
				servicePages: {
					anLayer: '../an-layer/an-layer',
					anTextAreaTip: '../anTextAreaTip/anTextAreaTip',
					anImage: '../an-image/an-image',
				}
			}
		},
		onLoad() {

		},
		methods: {
			goto(type){
				uni.navigateTo({
					url: this.servicePages[type]
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
