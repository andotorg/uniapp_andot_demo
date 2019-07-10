<template>
	<view>
		<image :src="url" :mode="mode" @error="imgError" :style="'width:'+(width<1?width*100+'%;':width+'px;')+'; height: '+(height<1?height*100+'%;':height+'px;')"></image>
	</view>
</template>

<script>
	export default {
		props: {
			src: {
				type: String,
				default: ''
			},
			alt: {
				type: String,
				default: ''
			},
			mode: {
				type: String,
				default: ''
			},
			width: {
				type: Number,
				default: 70
			},
			height: {
				type: Number,
				default: 90
			}
		},
		data() {
			return {
				url: this.src
			};
		},
		methods: {
			imgError(){
				this.url = this.alt;
			},
		}
	}
</script>

<style>

</style>
