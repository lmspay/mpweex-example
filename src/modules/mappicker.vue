<template>
	<div>
		<div class="group center">
			<div class="panel">
				<text class="text" v-if="value=='---'">{{value}}</text>
				<text class="text" v-else>地址：{{value.province+value.city+value.district+value.town+value.address}}</text>
			</div>
			<div class="panel">
				<text class="text">{{value=='---'?value:'经度：'+value.lng}}</text>
			</div>
			<div class="panel">
				<text class="text">{{value=='---'?value:'维度：'+value.lat}}</text>
			</div>
		</div>
		<div class="group">
			<mpwx-btn class="btn" label='Pick ' id="0" @onBtnClicked="pickMap"></mpwx-btn>
		</div>
	</div>
</template>

<script>
	const mappicker = weex.requireModule('mappicker');
	import MpwxBtn from "../mpwx-btn"
	export default {
		components: {
			MpwxBtn
		},
		data() {
			return {
				value: '---',
			}
		},
		methods: {
			pickMap() {
				mappicker.pick({}, event => {
					if (event.result === 'success') {
						this.value = event;
					}
				})
			}
		}
	}
</script>

<style scoped>
	.panel {
		/* height: 200px; */
		flex-direction: column;
		justify-content: center;
		border-width: 2px;
		border-style: solid;
		border-color: rgb(162, 217, 192);
		background-color: rgba(162, 217, 192, 0.2);
		margin-bottom: 24px;
	}

	.group {
		flex-direction: column;
		width: 650px;
		margin-left: 50px;
		margin-top: 50px;
	}

	.center {
		justify-content: center;
	}

	.text {
		font-size: 28px;
		color: #41B883;
		padding: 25px;
	}

	.btn {
		margin-bottom: 12px;
		margin-top: 12px;
	}
</style>
