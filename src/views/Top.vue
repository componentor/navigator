<template>
	<Box
		style="overflow:visible"
		backgroundColor="{`default`:{`xs`:{`light`:`#ede8e8ff`,`dark`:`#666464ff`},`md`:{`light`:`#00ff2aff`,`dark`:`#c44343ff`}},`hover`:{`xs`:{`light`:`#fff700ff`,`dark`:`#e6d23cff`}}}"
	>
		<Box
			:column="true"
			expand="true"
		></Box>
		<Box
			:column="true"
			style="overflow:visible"
		>
			<Navigator
				direction="right"
				iconSize="40px"
				orientation="Row"
				style="z-index:2;flex-grow:1"
				drop="down"
				backgroundColor="{`default`:{`xs`:{`light`:`#c95b5bff`,`dark`:`#804d4dff`},`md`:{`light`:`#ed2fd1ff`},`lg`:{`light`:`#ffd500ff`}},`hover`:{`xs`:{`light`:`#2932a6ff`}}}"
				color="{`default`:{`xs`:{`light`:`#e8dadaff`,`dark`:`#99f0afff`}}}"
				caretIcon="{`default`:{`xs`:{`light`:`--arrow-svg`}}}"
			>
				<NavItem title="A">
				</NavItem>
				<NavItem title="A">
				</NavItem>
				<NavItem
					title="B"
					icon="{`default`:{`xs`:{`light`:`--arrow-svg`,`dark`:`--close-svg`}}}"
				>
					<NavItem title="BA">
					</NavItem>
					<NavItem
						title="BB"
						itemDirection="right"
						backgroundColor="{`default`:{`xs`:{`light`:`#1ad6c3ff`}}}"
						textColor="{`default`:{`xs`:{`light`:`#f2c40aff`}}}"
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
							textColor="{`default`:{`xs`:{`light`:`#e60e0eff`}}}"
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
					title="B"
					icon="--menu-svg"
				>
					<NavItem title="BA">
					</NavItem>
					<NavItem
						title="BB"
						itemDirection="right"
						backgroundColor="{`default`:{`xs`:{`light`:`#1ad6c3ff`}}}"
						textColor="{`default`:{`xs`:{`light`:`#f2c40aff`}}}"
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
							textColor="{`default`:{`xs`:{`light`:`#e60e0eff`}}}"
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
					title="B"
					icon="--menu-svg"
				>
					<NavItem title="BA">
					</NavItem>
					<NavItem
						title="BB"
						itemDirection="right"
						backgroundColor="{`default`:{`xs`:{`light`:`#1ad6c3ff`}}}"
						textColor="{`default`:{`xs`:{`light`:`#f2c40aff`}}}"
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
							textColor="{`default`:{`xs`:{`light`:`#e60e0eff`}}}"
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
		</Box>
	</Box>
	<Box
		style="overflow:visible;z-index:0"
		expand="true"
	>
		<Navigator
			direction="right"
			iconSize="40px"
			orientation="Row"
			style="z-index:2;flex-grow:1"
			drop="down"
			textColor="{`default`:{`xs`:{`light`:`#de1d1dff`}}}"
			backgroundColor="{`default`:{`xs`:{`light`:`#cc7070ff`}},`hover`:{`xs`:{`light`:`#2932a6ff`}}}"
		>
			<NavItem title="A">
			</NavItem>
			<NavItem title="A">
			</NavItem>
			<NavItem
				title="B"
				icon="{`default`:{`xs`:{`light`:`--menu-svg`}}}"
			>
				<NavItem title="BA">
				</NavItem>
				<NavItem
					title="BB"
					itemDirection="right"
					backgroundColor="{`default`:{`xs`:{`light`:`#1ad6c3ff`}}}"
					textColor="{`default`:{`xs`:{`light`:`#f2c40aff`}}}"
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
						textColor="{`default`:{`xs`:{`light`:`#e60e0eff`}}}"
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
				title="B"
				icon="--menu-svg"
			>
				<NavItem title="BA">
				</NavItem>
				<NavItem
					title="BB"
					itemDirection="right"
					backgroundColor="{`default`:{`xs`:{`light`:`#1ad6c3ff`}}}"
					textColor="{`default`:{`xs`:{`light`:`#f2c40aff`}}}"
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
						textColor="{`default`:{`xs`:{`light`:`#e60e0eff`}}}"
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
				title="B"
				icon="--menu-svg"
			>
				<NavItem title="BA">
				</NavItem>
				<NavItem
					title="BB"
					itemDirection="right"
					backgroundColor="{`default`:{`xs`:{`light`:`#1ad6c3ff`}}}"
					textColor="{`default`:{`xs`:{`light`:`#f2c40aff`}}}"
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
						textColor="{`default`:{`xs`:{`light`:`#e60e0eff`}}}"
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
	</Box>
</template>
<script>
	import Box from '@vueplayio/box';
	import NavItem from '@/components/NavItem.vue';
	import Navigator from '@/App.vue';
	export default {
		components: {
			Box: Box,
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