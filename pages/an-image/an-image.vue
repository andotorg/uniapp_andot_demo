<template>
	<view>
		<view v-for="(item, index) in urls" :key="index">
			<an-image :src="item+'?andot=lucas'" :alt="defaultImg"></an-image>
		</view>
	</view>
</template>

<script>
	import anImage from '../../components/an-image/an-image.vue'
	
	export default {
		components: {
			anImage
		},
		data() {
			return {
				urls: [
					'https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=1315127236,2525556170&fm=27&gp=0.jpg',
					'https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=2839013524,2802969008&fm=26&gp=0.jpg',
					'',
					'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1562837113557&di=fcdc23dc4bd3071e2d529b977bf794c1&imgtype=0&src=http%3A%2F%2Fdik.img.kttpdq.com%2Fpic%2F46%2F32134%2F0a2e134eeef1754c_1366x768.jpg',
					'https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=388393289,867899239&fm=27&gp=0.jpg',
				],
				defaultImg: 'https://avatars3.githubusercontent.com/u/25116294?s=460&v=4'
			}
		},
		methods: {
			
		}
	}
</script>

<style>

</style>
