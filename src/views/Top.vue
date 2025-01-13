<template>
	<Demo
		iconSize="45px"
		direction="Row"
	>
		<NavItem title="A">
		</NavItem>
		<NavItem
			title="B"
			icon="--menu-svg"
		>
			<NavItem title="BA">
			</NavItem>
			<NavItem title="BB">
				<NavItem
					title="BBA"
					icon="--close-svg"
					iconReverse="true"
				>
				</NavItem>
				<NavItem
					title="BBC"
					icon="--menu-svg"
				></NavItem>
				<NavItem
					title="BB"
					icon="--menu-svg"
				>
					<NavItem title="BBA">
					</NavItem>
					<NavItem title="BBC"></NavItem>
					<NavItem title="BBD"></NavItem>
				</NavItem>
				<NavItem title="BBD"></NavItem>
			</NavItem>
			<NavItem
				title="BC"
				icon="--menu-svg"
			></NavItem>
			<NavItem title="BD"></NavItem>
		</NavItem>
		<NavItem
			title="C"
			icon="--close-svg"
		>
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
<style scoped>
	* {
		--menu-svg: url(@/assets/menu.svg);
		--close-svg: url(@/assets/close.svg);
		--arrow-svg: url(@/assets/arrow.svg);
	}

</style>