<!-- ParentComponent.vue -->
<template>
	<view>	
		<index v-if="activeTab === 'index'" ></index>
		<user v-if="activeTab === 'user'" ></user>
		<tabbar @change="handleTabChange" ></tabbar>
	</view>
</template>

<script>

	export default {
		data() {
			return {
				activeTab: 'index',
			};
		},
		
		methods: {
			handleTabChange(tab) {
				console.log("当前状态是：", tab);
				this.activeTab = tab;
				console.log("当前的activeTab是：", this.activeTab);
			},
		},
	};
</script>
<style>
	
</style>