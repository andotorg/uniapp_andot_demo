<template xlang="wxml" minapp="mpvue">
	<view class="an-qrcode">
		<canvas 
			:canvas-id="aid" 
			:id="aid"
			:style="'width: '+size+'px; height: '+size+'px;'" 
			v-show="show" />
	</view>
</template>

<script>
	/**
	 * 生成二维码
	 * API很简单，期待后期升级吧！
	 * @author lucas
	 * @date 2019-8-17 10:25:58
	 * */
	import qrcode from './an-qrcode.js'
	export default {
		name: "Anqrcode",
		props: {
			show: {
				type: Boolean,
				default: true
			},
			aid: {
				type: String,
				default: 'an-qrcode-canvas'
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
						marginLeft: 50,//设置条形码周围的左边距
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
			size: {
				type: Number,
				default: 250
			},
			level: {
				type: Number,
				default: 2
			}
		},
		methods: {
			_makeCode(n, o) {
				let that = this
				this.fixMargin();
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
				uni.showLoading({
					title: '二维码生成中'
				})
				if (this.onval) {
					if (n != o && !this._empty(n)) {
						try{
							qrcode.api.draw(this.val, {
								ctx: uni.createCanvasContext(this.aid, this),
								width: this.convert_length(this.size),
								height: this.convert_length(this.size),
								frontground: this.options.lineColor,
							}, this.size, this.level)
							uni.hideLoading();
						}catch(e){
							//TODO handle the exception
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
			},
			convert_length(length) {
				return Math.round(wx.getSystemInfoSync().windowWidth * length / 750);
			}
		},
		watch: {
			val: function (n, o) {
				this._makeCode(n, o);
			}
		},
		mounted: function () {
			if (this.loadMake) {
				let that = this;
				setTimeout(function(){
					that._makeCode(that.val, '');
				}, 1000);
			}
		},
	}
</script>
<style>
	.an-qrcode {
		width: 100%;
		display: flex;
		justify-content: center;
	}
</style>
