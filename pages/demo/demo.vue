<template>
	<view>
		<view>{{user_name}}</view>
		<view v-for="one in tel">{{one}}</view>
		
		<view v-if="age >= 18">
			<button @tap="signUp()">我要报名</button>
		</view>
		
		<view>
			<input type="text" v-model="address" placeholder="输入地址"/>
		</view>
		<view>{{address}}</view>
	</view>

</template>

<script>
	export default {
		data() {
			return {
				user_name: "Scott",
				tel: ["13312345678", "15912345678"],
				age: 14,
				address: ""
			};
		},
		methods:{
			signUp: function() {
				uni.showToast({
					title:"点击了按钮"
				})
			}
		}
	}
</script>

<style>

</style>

