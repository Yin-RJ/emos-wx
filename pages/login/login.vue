<template>
	<view>
		<image src="../../static/logo-1.png" class="logo" mode="widthFix"></image>
		<view class="logo-title">EMOS企业办公</view>
		<view class="logo-subtitle">Ver 2050.2</view>
		<button class="login-btn" open-type="getUserInfo" @tap="login()">登录系统</button>
		<view class="register-container">
			没有账号？
			<text class="register" @tap="toRegister()">立即注册</text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {

			}
		},
		methods: {
			login() {
				let that = this;
				uni.login({
					provider: "weixin",
					success: function(resp) {
						let code = resp.code;
						that.ajax(that.url.login, "POST", {
							"code": code
						}, function(resp) {
							let permission = resp.data.permission;
							uni.setStorageSync('permission', permission);
							//TODO 跳转到登陆页面
							uni.showToast({
								title: "登录成功"
							})
						})
					},
					fail: function(e) {
						console.log(e)
						uni.showToast({
							icon: "none",
							title: "执行异常"
						})
					}
				})
			},
			toRegister() {
				// 跳转到注册页面
				uni.navigateTo({
					url: "../register/register"
				})
			}
		}
	}
</script>

<style lang="less">
	@import url("login.less");
</style>
