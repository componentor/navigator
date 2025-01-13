<template>
	<Demo
		iconSize="45px"
		direction="Row"
	>
		<NavItem title="A">
		</NavItem>
		<NavItem title="B">
			<NavItem title="BA">
			</NavItem>
			<NavItem title="BB">
				<NavItem title="BBA">
				</NavItem>
				<NavItem title="BBC"></NavItem>
				<NavItem title="BBD"></NavItem>
			</NavItem>
			<NavItem title="BC"></NavItem>
			<NavItem title="BD"></NavItem>
		</NavItem>
		<NavItem title="C">
		</NavItem>
		<NavItem title="D"></NavItem>
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