<template>
	<view>
		<view style="margin-top: 100upx;">
			<button type="default" @click="showMsg('info')">默认</button>
		</view>
		<view>
			<button type="default" @click="showMsg('success')">成功</button>
		</view>
		<view>
			<button type="default" @click="showMsg('warn')">警告</button>
		</view>
		<view>
			<button type="default" @click="showMsg('error')">错误</button>
		</view>
		<an-layer ref="anRef" autoClose="true" timer="3" :type="type">
			<text>{{message}}</text>
		</an-layer>
	</view>
</template>

<script>
	import anLayer from '@/components/an-layer/an-layer'

	export default {
		components:{
			anLayer
		},
		data() {
			return {
				type: 'info',
				message: 'Hello Andot'
			}
		},
		methods: {
			showMsg(type){
				this.type = type;
				this.$refs.anRef.show();
			}
		}
	}
</script>

<style>
	button{
		margin: 20upx;
	}
</style>
