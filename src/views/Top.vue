<template>
	<Demo
		iconSize="45px"
		direction="Row"
	>
		<NavItem>
		</NavItem>
		<NavItem>
			<NavItem></NavItem>
			<NavItem></NavItem>
			<NavItem></NavItem>
		</NavItem>
		<NavItem>
		</NavItem>
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