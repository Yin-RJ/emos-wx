<template>
	<view>
		<image src="../../static/logo-2.png" mode="widthFix" class="logo"></image>
		<view class="register-container">
			<input type="text" placeholder="输入你的邀请码" class="register-code" maxlength="6" v-model="registerCode" />
			<view class="register-desc">
				管理员创建员工账号后，从个人邮箱获取注册邀请码
			</view>
			<button class="register-btn" open-type="getUserInfo" @tap="register()">立即注册</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				registerCode: null
			}
		},
		methods: {
			register() {
				
			}
		}
	}
</script>

<style lang="less">
	@import url("register.less");
</style>
