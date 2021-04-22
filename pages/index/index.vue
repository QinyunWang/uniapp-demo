<template>
	<view class="container">
		<img :src="src" class="avatar" alt="avatar" />
		<view>你好<span class="name">{{ name }}</span></view>
		<view class="intro">你现在的位置： {{ city }}</view>
	</view>
</template>

<script>
	export default {
		onLoad() {
			var _this = this;
			uni.getLocation({
				success(res) {
					_this.city = res.city
				}
			})
			
			tt.login({
				success(res) {
					tt.getUserInfo({
						success(res) {
							console.log(res)
							_this.name = res.userInfo.nickName
							_this.src = res.userInfo.avatarUrl
						},
						fail(res) {
							console.warn(res)
						}
					})
				}
			})
		},
		data() {
			return {
				city: '未知',
				name: 'Someone',
				src: '',
			}
		},
		methods: {

		}
	}
</script>

<style>
	.container {
		padding: 20px;
		font-size: 14px;
		line-height: 24px;
	}
	
	.avatar {
		float: right;
		width: 100px;
		height: 100px;
		border-radius: 50px;
	}
	
	.name {
		margin-top: 50px;
		display: inline-block;
		color: #F0AD4E;
	}
</style>
