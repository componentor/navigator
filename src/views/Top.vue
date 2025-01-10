<template>
	<Demo iconSize="145px">
		<NavItem></NavItem>
		<NavItem>
			<NavItem></NavItem>
			<NavItem></NavItem>
			<NavItem></NavItem>
		</NavItem>
		<NavItem></NavItem>
		<NavItem></NavItem>
	</Demo>
</template>
<script>
	import NavItem from '@/components/NavItem.vue';
	import Demo from '@/App.vue';
	export default {
		components: {
			NavItem: NavItem,
			Demo: Demo
		},
		data: () => ({})
	};

</script>
<style scoped></style>