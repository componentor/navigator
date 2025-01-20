<template>
	<Row style="overflow:visible">
		<Column expand="true"></Column>
		<Column style="overflow:visible">
			<Navigator
				direction="right"
				iconSize="40px"
				orientation="Row"
				style="z-index:2;flex-grow:1"
				drop="down"
				textColor="{`default`:{`xs`:{`light`:`#1efc7bff`}}}"
				backgroundColor="{`default`:{`xs`:{`light`:`#db6363ff`}},`hover`:{`xs`:{`light`:`#cf9b9bff`}}}"
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
					<NavItem
						title="BB"
						itemDirection="right"
					>
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
							itemDirection="left"
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
		</Column>
	</Row>
	<Row
		style="overflow:visible"
		expand="true"
	>
	</Row>
</template>
<script>
	import Column from '@vueplayio/column';
	import Row from '@vueplayio/row';
	import NavItem from '@/components/NavItem.vue';
	import Navigator from '@/App.vue';
	export default {
		components: {
			Column: Column,
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