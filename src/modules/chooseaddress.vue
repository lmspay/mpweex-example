<template>
	<list>
		<cell style="padding-top: 20px;">
			<text class="text">所在地区：{{province}}{{city}}{{district}}{{town}}</text>
			<text class="text">详细地址：{{address}}</text>
			<text class="text">收货人：{{userName}}</text>
			<text class="text">电话：{{phoneNo}}</text>
			<text class="text">性别：{{gender}}</text>
			<div class="group center">
				<mpwx-btn class="btn" label='选择地址 ' id="0" @onBtnClicked="choose()"></mpwx-btn>
			</div>
		</cell>
	</list>
</template>

<script>
	const chooseaddress = weex.requireModule('chooseaddress');
	const actionSheet = weex.requireModule('actionSheet');
	import MpwxBtn from "../mpwx-btn";
	export default {
		components: {
			MpwxBtn
		},
		data() {
			return {
				province: '',
				city: '',
				district: '',
				town: '',
				address: '',
				phoneNo: '',
				userName: '',
				gender: '',
			}
		},
		methods: {
			choose() {
				chooseaddress.pick({

				}, e=> {
					if(e.ok) {
						this.province = e.data.province;
						this.city = e.data.city;
						this.district = e.data.district;
						this.town = e.data.town;
						this.address = e.data.address;
						this.phoneNo = e.data.phoneNo;
						this.userName = e.data.userName;
						this.gender = (e.data.gender == 0 ? '先生' : '女士');
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
