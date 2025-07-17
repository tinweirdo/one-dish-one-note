<template>
	<view class="page-container">
		<!-- 顶部用户信息区 -->
		<Header />
		<!-- 菜单列表区 -->
		<MenuList />
	</view>
</template>

<script>
import { Header } from '../../src/components/header.vue';
import { MenuList } from '../../src/components/menulist.vue';


export default {
	components: {
		Header,
		MenuList
	}
}
</script>

<style scoped>
.page-container {
	background: #fff;
	height: 100vh;
}
</style>
