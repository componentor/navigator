<template>
	<Row
		style="overflow:visible"
		expand="true"
	>
		test
	</Row>
	<Row style="z-index:2;overflow:visible">
		<Navigator
			direction="right"
			iconSize="40px"
			orientation="Column"
			style="z-index:2;flex-grow:1"
			drop="up"
			forceOpen="true"
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
						iconReverse="false"
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
		</Navigator>
	</Row>
</template>
<script>
	import Row from '@vueplayio/row';
	import NavItem from '@/components/NavItem.vue';
	import Navigator from '@/App.vue';
	export default {
		components: {
			Row: Row,
			NavItem: NavItem,
			Navigator: Navigator
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