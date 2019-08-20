<template>
	<view class="an-barcode">
		<view :style="'width: '+options.width+'px; height: '+options.height+'px;'">
			<canvas 
				:canvas-id="aid" 
				:id="aid"
				:style="'width: '+options.width+'px; height: '+options.height+'px;'" 
				v-show="show" />
		</view>
		<!-- margin-top: '+options.marginTop+'px; margin-right: '+options.marginRight+'px; margin-bottom: '+options.marginBottom+'px; margin-left: '+options.marginLeft+'px;' -->
		
	</view>
</template>

<script>
	/**
	 * 生成条形码，对比tki-barcode,解决了IOS中切换文字重新刷新条形码之后的模糊情况
	 * API很简单，期待后期升级吧！
	 * @author lucas
	 * @date 2019-8-17 10:25:58
	 * */
	import barcode from './an-barcode.js'
	export default {
		name: "AnBarcode",
		props: {
			show: {
				type: Boolean,
				default: true
			},
			aid: {
				type: String,
				default: 'an-barcode-canvas'
			},
			val: {
				type: String,
				default: 'lucas'
			},
			unit: {
				type: String,
				default: ''
			},
			format: {
				type: String,
				default: 'CODE128'
			},
			options: {
				type: Object,
				default: function () {
					return {
						width: 250,//设置条之间的宽度
						height: 50,//高度
						lineColor: "#000000",//设置条形码的颜色
						background: "#FFFFFF",//设置条形码的背景色
						displayValue: false,//是否在条形码下方显示文字
						text: "",//覆盖显示的文本
						textAlign: "center",//设置文本的水平对齐方式
						textPosition: "bottom",//设置文本的垂直位置
						textMargin: 0,//设置条形码和文本之间的间距
						fontSize: 24,//设置文本的大小
						fontColor: "#000000",//设置文本的颜色
						margin: 0,//设置条形码周围的空白边距
						marginTop: undefined,//设置条形码周围的上边距
						marginBottom: undefined,//设置条形码周围的下边距
						marginLeft: undefined,//设置条形码周围的左边距
						marginRight: undefined,//设置条形码周围的右边距
					}
				}
			},
			onval: {
				type: Boolean,
				default: false
			},
			loadMake: {
				type: Boolean,
				default: true
			},
		},
		methods: {
			_makeCode(n, o) {
				let that = this
				that.fixMargin();
				if (that.unit == "upx") {
					if (that.options.width) {
						that.options.width = uni.upx2px(that.options.width)
					}
					if (that.options.height) {
						that.options.height = uni.upx2px(that.options.height)
					}
					if (that.options.fontSize) {
						that.options.fontSize = uni.upx2px(that.options.fontSize)
					}
				}
				if (that.onval) {
					if (n != o && !that._empty(n)) {
						try{
							console.log('[try]===', n, o, that.aid)
							barcode.code128(uni.createCanvasContext(that.aid, that), n, {
								width: that.options.width, 
								height: that.options.height,
								frontground: that.options.lineColor,
								background: that.options.background,
							})
							uni.hideLoading();
						}catch(e){
							uni.hideLoading();
						}
					}else{
						uni.hideLoading();
						uni.showToast({
							icon: 'none',
							title: '文本不能为空'
						})
					}
				}
			},
			_saveCode() {
				let that = this;
				if (this.result != "") {
					uni.saveImageToPhotosAlbum({
						filePath: that.result,
						success: function () {
							uni.showToast({
								title: '条形码保存成功',
								icon: 'success',
								duration: 2000
							});
						}
					});
				}
			},
			_empty(v) {
				let tp = typeof v,
					rt = false;
				if (tp == "number" && String(v) == "") {
					rt = true
				} else if (tp == "undefined") {
					rt = true
				} else if (tp == "object") {
					if (JSON.stringify(v) == "{}" || JSON.stringify(v) == "[]" || v == null) rt = true
				} else if (tp == "string") {
					if (v == "" || v == "undefined" || v == "null" || v == "{}" || v == "[]") rt = true
				} else if (tp == "function") {
					rt = false
				}
				return rt
			},
			fixMargin() {
				this.options.marginTop = this.options.marginTop == undefined ? this.options.margin : this.options.marginTop;
				this.options.marginBottom = this.options.marginBottom == undefined ? this.options.margin : this.options.marginBottom;
				this.options.marginRight = this.options.marginRight == undefined ? this.options.margin : this.options.marginRight;
				this.options.marginLeft = this.options.marginLeft == undefined ? this.options.margin : this.options.marginLeft;
			}
		},
		watch: {
			val: function (n, o) {
				uni.showLoading({
					title: '条码生成中'
				})
				let that = this;
				that._makeCode(n, o);
			}
		},
		created: function () {
			if (this.loadMake) {
				uni.showLoading({
					title: '条码生成中'
				})
				let that = this;
				setTimeout(function(){
					that._makeCode(that.val, '00');
				}, 1000)
			}
		},
	}
</script>
<style>
	.an-barcode {
		width: 100%;
		display: flex;
		justify-content: center;
	}
</style>
