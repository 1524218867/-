<template>
	<div class="tabbar-content">
		<div class="tabbar-btn">
			<button class="btnaft" :class="{ active: activeTab === 'index' }" @click="changeTab('index')">
				<!-- 判断当前激活的 tab，动态切换图标 -->
				<template v-if="activeTab === 'index'">
					<img src="@/static/index-active.png" alt="active-icon" />
				</template>
				<template v-else>
					<img src="@/static/index.png" alt="default-icon" />
				</template>
			</button>
			<button class="btnaft" :class="{ active: activeTab === 'user' }" @click="changeTab('user')">
				<template v-if="activeTab === 'user'">
					<img src="@/static/user-active.png" alt="user-active-icon" />
				</template>
				<template v-else>
					<img src="@/static/user.png" alt="user-default-icon" />
				</template>
			</button>
		</div>
	</div>
</template>


<script>
	export default {
		data() {
			return {
				activeTab: 'index', // 默认活动 tab
			};
		},
		methods: {
			changeTab(tab) {
				console.log('Change tab to:', tab); // 调试输出
				this.activeTab = tab; // 更新活动 tab
				this.$emit('change', tab); // 触发 change 事件
			},
		},
		mounted() {
			console.log('打印了tabbar');
		}
	};
</script>

<style>
	
	.tabbar-content {
		height: 13vh;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}
	
	.tabbar-btn {
		display: flex;
		background-color: #E5E7E8;
		width: 80%;
		height: 75%;
		border-radius: 15px;
		flex-direction: row;
		align-items: center;
		justify-content: space-around;
		padding: 3px 0;
	}
	
	.tabbar-btn>button {
		height: 90%;
		width: 30%;
		border-radius: 15px;
		background-color: #E5E7E8;
		margin: 0 5px;
		display: flex;
		align-items: center;
		justify-content: center;
	}
	.tabbar-btn>button>image{
		height: 25px;
		width: 25px;
	}
	.tabbar-btn>button.active {
		background-color: #333;
		color: #fff;
	}
	
	.btnaft::after {
		border: none;
	}

</style>