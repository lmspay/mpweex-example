<template>
	<div>
		<div class="group">
			<image class="group-image" :src="item" v-for="(item,index) in listImage" :key="index" @click="pickShow(index)"></image>
		</div>
		<div class="group center">
			<mpwx-btn class="btn" label='点击图片预览 ' id="0" @onBtnClicked="pickShow()"></mpwx-btn>
		</div>
	</div>
</template>

<script>
	const photopreview = weex.requireModule('photopreview');
	import MpwxBtn from "../mpwx-btn"
	export default {
		components: {
			MpwxBtn
		},
		data() {
			return {
				value: '---',
				listImage: ['mpweex://images/defcoms.png',
					'mpweex://images/defmods.png',
					'mpweex://images/demos.png',
					'mpweex://images/logo.png',
					'mpweex://images/seniorcms.png'
				]
			}
		},
		methods: {
			pickShow(index = 0) {
				var options = {
					startIndex: index,
					urls: this.listImage,
				}
				photopreview.show(options, event => {
					if (event.result === 'success') {
						this.value = event;
					}
				})
			}
		}
	}
</script>

<style scoped>
	.group {
		flex-direction: row;
		flex-wrap: wrap;
		margin-left: 50px;
		margin-top: 50px;
	}

	.group-image {
		width: 240px;
		height: 240px;
		margin:0 100px 24px 0;
	}
	.center{
		justify-content: center;
	}
	.btn {
		margin-bottom: 12px;
		margin-top: 12px;
	}
</style>
