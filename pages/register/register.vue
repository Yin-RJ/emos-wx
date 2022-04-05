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
				registerCode: null,
				nickname: '',
				avatar_url: '',
				code: ''
			}
		},
		methods: {
			register() {
				let that = this;
				if (that.registerCode == null || that.registerCode.length == 0) {
					uni.showToast({
						title: '邀请码不能为空',
						icon: 'none'
					});
					return;
				} else if (/^[0-9]{6}$/.test(that.registerCode) == false) {
					uni.showToast({
						title: '邀请码必须是6为数字',
						icon: 'none'
					});
					return;
				}

				uni.login({
					provider: "weixin",
					success: function(resp) {
						that.code = resp.code;
						console.log(that.code);
					}
				});
				
				uni.getUserProfile({
					desc: "获取用户信息",
					success: function(resp) {
						console.log(resp);
						that.nickname = resp.userInfo.nickName;
						that.avatar_url = resp.userInfo.avatarUrl;
						let data = {
							code: that.code,
							nickname: that.nickname,
							photo: that.avatar_url,
							registerCode: that.registerCode
						};
						that.ajax(that.url.register, 'POST', data, function(resp) {
							let permission = resp.data.permission;
							uni.setStorageSync('permission', permission);
							//跳转到index页面
						});
				
					},
					fail: function(res) {}
				});
			}
		}
	}
</script>

<style lang="less">
	@import url("register.less");
</style>
