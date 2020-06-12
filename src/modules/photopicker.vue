<template>
	<list>
		<cell>
			<image :style="{height:fileHeight,width:fileWidth}" class="group-image" :src="filePath" @click="show()"></image>
			<text class="text">图片名：{{fileName}}</text>
			<text class="text">图片路径：{{filePath}}</text>
			<text class="text">图片大小：{{fileSize}}</text>
			<text class="text">图片高：{{fileHeight}}</text>
			<text class="text">图片宽：{{fileWidth}}</text>
			<div class="group center">
				<mpwx-btn class="btn" label='选择图片 ' id="0" @onBtnClicked="choose()"></mpwx-btn>
			</div>
		</cell>
	</list>
</template>

<script>
	const photopicker = weex.requireModule('photopicker');
	const actionSheet = weex.requireModule('actionSheet');
	const photopreview = weex.requireModule('photopreview');
	import MpwxBtn from "../mpwx-btn";
	export default {
		components: {
			MpwxBtn
		},
		data() {
			return {
				filePath: '---',
				fileName: '---',
				fileSize: '---',
				fileHeight: '---',
				fileWidth: '---',
			}
		},
		methods: {
			show() {
				var options = {
					urls: [this.filePath]
				}
				photopreview.show(options, function(event) {

				})
			},
			choose() {
				var items = [{
						'type': 0,
						'message': '从相册中选择'
					},
					{
						'type': 1,
						'message': '取消'
					},
					{
						'type': 2,
						'message': '拍摄选择照片'
					}
				];
				var self = this;
				actionSheet.create({
					'items': items,
					'title': '提示',
					'message': '选择上传图片'
				}, function(ret) {
					var result = ret.result;
					if (result == 'success') {
						if (ret.data.index == 0) {
							self.choosePicture()
							//从相册选择
						} else if (ret.data.index == 2) {
							//拍照
							self.shotPicture()
						}
					}
				});
			},
			// 拍摄0
			shotPicture() {
				var self = this;
				photopicker.pick({
					type: 0,
					base64: false,
				}, function(event) {
					if (event.result == 'success') {
						self.filePath = event.filePath;
						self.fileName = event.fileName;
						self.fileSize = (event.fileSize / 1024).toFixed(2) + 'kb';
						if (event.fileWidth > 702) {
							self.fileHeight = event.fileHeight / (event.fileWidth / 702) + 'px';
							self.fileWidth = '702px';
						} else {
							self.fileWidth = event.fileWidth + 'px';
							self.fileHeight = event.fileHeight + 'px';
						}
					}
				});
			},
			// 选择1
			choosePicture() {
				var self = this;
				photopicker.pick({
					type: 1,
					base64: false,
				}, function(event) {
					if (event.result == 'success') {
						self.filePath = event.filePath;
						self.fileName = event.fileName;
						self.fileSize = (event.fileSize / 1024).toFixed(2) + 'kb';
						if (event.fileWidth > 702) {
							self.fileHeight = event.fileHeight / (event.fileWidth / 702) + 'px';
							self.fileWidth = '702px';
						} else {
							self.fileWidth = event.fileWidth + 'px';
							self.fileHeight = event.fileHeight + 'px';
						}
					}
				});
			}
		}
	}
</script>

<style scoped>
	.group {
		margin-left: 24px;
		margin-top: 50px;
	}

	.group-image {
		margin: 24px 24px 100px 24px;
	}

	.center {
		width: 702px;
		justify-content: center;
	}

	.text {
		border-width: 2px;
		border-style: solid;
		border-color: rgb(162, 217, 192);
		background-color: rgba(162, 217, 192, 0.2);
		font-size: 28px;
		color: #41B883;
		padding: 25px;
		width: 702px;
		text-align: left;
		margin:0 24px 24px 24px;
	}

	.btn {
		margin-bottom: 12px;
		margin-top: 12px;
	}
</style>
