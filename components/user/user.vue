<template>
	<view class="user-content">
		<view>
			<u-avatar :src="src" size="large"></u-avatar>
			<u-avatar :text="text"></u-avatar>
		</view>
		<p>user</p>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				src: 'https://blog.csdn.net/dQCFKyQDXYm3F8rB0/article/details/141217428?spm=1000.2115.3001.5926',
				text: '无头像',
				
			}
		},
		methods: {

		},
		mounted() {
			console.log("打印了user");
		}
	}
</script>

<style>
	.user-content {
		height: 87vh;
	}
</style>