<template>
	<view class="wx-qrcode">
		<canvas v-if="!codeImg" type="2d" style="display: none;" id="myQrcode"></canvas>
		<image v-else :src="codeImg" mode="" style="width: 100%;height: 100%;"></image>
	</view>
</template>

<script>
	import drawQrcode from './weapp.qrcode.esm.js';
	export default {
		name: 'wx-qrcode',
		props: {
			// 二维码中间logo图片
			imageUrl: {
				type: String,
				default:　''
			},
			// logo宽
			imageWidth: {
				type: [String, Number],
				default: 50
			},
			// logo图片高
			imageHeight: {
				type: [String, Number],
				default: 50
			},
			// 中间logo是否是圆形
			isRound: {
				type: Boolean,
				default: false,
			},
			// 二维码内容
			text: {
				type: String,
				required: true
			},
			// 二维码与四周空白内边距
			padding: {
				type: [String, Number],
				default: 20
			},
			// 二维码与四周的padding颜色
			paddingColor: {
				type: String,
				default: '#fff'
			},
			// 二维码背景颜色
			background: {
				type: String,
				default: '#fff'
			},
			// 二维码颜色
			foreground: {
				type: String,
				default: '#000'
			}
		},
		mounted() {
			this.drawCode()
		},
		data() {
			return {
				codeImg: ''
			};
		},
		methods:{
			// 微信小程序二维码生成
			drawCode() {
				const _this = this
				const query = uni.createSelectorQuery().in(this)
				query.select('#myQrcode')
					.fields({
						node: true,
						size: true
					})
					.exec(async (res) => {
						var canvas = res[0].node
						var options = {
							canvas: canvas,
							canvasId: 'myQrcode',
							padding: _this.padding,
							paddingColor: _this.paddingColor,
							background: _this.background,
							foreground: _this.foreground,
							text: _this.text,
						}
						if (_this.imageUrl){
							var img = canvas.createImage();
							img.src = _this.imageUrl
				
							img.onload = function() {
								// img.onload完成后才能调用 drawQrcode方法
								options.image = {
									imageResource: img,
									width: _this.imageWidth, // 建议不要设置过大，以免影响扫码
									height: _this.imageHeight, // 建议不要设置过大，以免影响扫码
									round: _this.isRound // Logo图片是否为圆形
								}
								drawQrcode(options)
								_this.codeImg = canvas.toDataURL("image/png")							
							}
						} else {
							drawQrcode(options)
							_this.codeImg = canvas.toDataURL("image/png")							
						}
					})
			}
		}
	}
</script>

<style lang="scss" scoped>
.wx-qrcode{
	width: 100%;
	height: 100%;
}
</style>
