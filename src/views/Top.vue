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
				backgroundColorDrop="{`default`:{`xs`:{`light`:`#db1fd5ff`}}}"
			>
				<Link title="A">
				</Link>
				<Link title="A">
				</Link>
				<Link
					title="B"
					icon="{`default`:{`xs`:{`light`:`--arrow-svg`,`dark`:`--close-svg`}}}"
				>
				<Link title="BA">
				</Link>
				<Link
					title="BB"
					itemDirection="right"
					backgroundColor="{`default`:{`xs`:{`light`:`#1ad6c3ff`}}}"
					textColor="{`default`:{`xs`:{`light`:`#f2c40aff`}}}"
				>
				<Link
					title="BBA"
					icon="--close-svg"
					iconReverse="false"
				>
				</Link>
				<Link
					title="BBC"
					icon="--menu-svg"
				>
				</Link>
				<Link
					title="BB"
					icon="--menu-svg"
					itemDirection="left"
					textColor="{`default`:{`xs`:{`light`:`#e60e0eff`}}}"
				>
				<Link title="BBA">
				</Link>
				<Link title="BBC">
				</Link>
				<Link title="BBD">
				</Link>
				</Link>
				<Link title="BBD">
				</Link>
				</Link>
				<Link
					title="BC"
					icon="--menu-svg"
				>
				</Link>
				<Link title="BD">
				</Link>
				</Link>
				<Link
					title="B"
					icon="--menu-svg"
				>
				<Link title="BA">
				</Link>
				<Link
					title="BB"
					itemDirection="right"
					backgroundColor="{`default`:{`xs`:{`light`:`#1ad6c3ff`}}}"
					textColor="{`default`:{`xs`:{`light`:`#f2c40aff`}}}"
				>
				<Link
					title="BBA"
					icon="--close-svg"
					iconReverse="false"
				>
				</Link>
				<Link
					title="BBC"
					icon="--menu-svg"
				>
				</Link>
				<Link
					title="BB"
					icon="--menu-svg"
					itemDirection="left"
					textColor="{`default`:{`xs`:{`light`:`#e60e0eff`}}}"
				>
				<Link title="BBA">
				</Link>
				<Link title="BBC">
				</Link>
				<Link title="BBD">
				</Link>
				</Link>
				<Link title="BBD">
				</Link>
				</Link>
				<Link
					title="BC"
					icon="--menu-svg"
				>
				</Link>
				<Link title="BD">
				</Link>
				</Link>
				<Link
					title="B"
					icon="--menu-svg"
				>
				<Link title="BA">
				</Link>
				<Link
					title="BB"
					itemDirection="right"
					backgroundColor="{`default`:{`xs`:{`light`:`#1ad6c3ff`}}}"
					textColor="{`default`:{`xs`:{`light`:`#f2c40aff`}}}"
				>
				<Link
					title="BBA"
					icon="--close-svg"
					iconReverse="false"
				>
				</Link>
				<Link
					title="BBC"
					icon="--menu-svg"
				>
				</Link>
				<Link
					title="BB"
					icon="--menu-svg"
					itemDirection="left"
					textColor="{`default`:{`xs`:{`light`:`#e60e0eff`}}}"
				>
				<Link title="BBA">
				</Link>
				<Link title="BBC">
				</Link>
				<Link title="BBD">
				</Link>
				</Link>
				<Link title="BBD">
				</Link>
				</Link>
				<Link
					title="BC"
					icon="--menu-svg"
				>
				</Link>
				<Link title="BD">
				</Link>
				</Link>
				<Link
					title="C"
					icon="--close-svg"
				>
				</Link>
				<Link title="D">
				</Link>
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
			<Link title="A">
			</Link>
			<Link title="A">
			</Link>
			<Link
				title="B"
				icon="{`default`:{`xs`:{`light`:`--menu-svg`}}}"
			>
			<Link title="BA">
			</Link>
			<Link
				title="BB"
				itemDirection="right"
				backgroundColor="{`default`:{`xs`:{`light`:`#1ad6c3ff`}}}"
				textColor="{`default`:{`xs`:{`light`:`#f2c40aff`}}}"
			>
			<Link
				title="BBA"
				icon="--close-svg"
				iconReverse="false"
			>
			</Link>
			<Link
				title="BBC"
				icon="--menu-svg"
			>
			</Link>
			<Link
				title="BB"
				icon="--menu-svg"
				itemDirection="left"
				textColor="{`default`:{`xs`:{`light`:`#e60e0eff`}}}"
			>
			<Link title="BBA">
			</Link>
			<Link title="BBC">
			</Link>
			<Link title="BBD">
			</Link>
			</Link>
			<Link title="BBD">
			</Link>
			</Link>
			<Link
				title="BC"
				icon="--menu-svg"
			>
			</Link>
			<Link title="BD">
			</Link>
			</Link>
			<Link
				title="B"
				icon="--menu-svg"
			>
			<Link title="BA">
			</Link>
			<Link
				title="BB"
				itemDirection="right"
				backgroundColor="{`default`:{`xs`:{`light`:`#1ad6c3ff`}}}"
				textColor="{`default`:{`xs`:{`light`:`#f2c40aff`}}}"
			>
			<Link
				title="BBA"
				icon="--close-svg"
				iconReverse="false"
			>
			</Link>
			<Link
				title="BBC"
				icon="--menu-svg"
			>
			</Link>
			<Link
				title="BB"
				icon="--menu-svg"
				itemDirection="left"
				textColor="{`default`:{`xs`:{`light`:`#e60e0eff`}}}"
			>
			<Link title="BBA">
			</Link>
			<Link title="BBC">
			</Link>
			<Link title="BBD">
			</Link>
			</Link>
			<Link title="BBD">
			</Link>
			</Link>
			<Link
				title="BC"
				icon="--menu-svg"
			>
			</Link>
			<Link title="BD">
			</Link>
			</Link>
			<Link
				title="B"
				icon="--menu-svg"
			>
			<Link title="BA">
			</Link>
			<Link
				title="BB"
				itemDirection="right"
				backgroundColor="{`default`:{`xs`:{`light`:`#1ad6c3ff`}}}"
				textColor="{`default`:{`xs`:{`light`:`#f2c40aff`}}}"
			>
			<Link
				title="BBA"
				icon="--close-svg"
				iconReverse="false"
			>
			</Link>
			<Link
				title="BBC"
				icon="--menu-svg"
			>
			</Link>
			<Link
				title="BB"
				icon="--menu-svg"
				itemDirection="left"
				textColor="{`default`:{`xs`:{`light`:`#e60e0eff`}}}"
			>
			<Link title="BBA">
			</Link>
			<Link title="BBC">
			</Link>
			<Link title="BBD">
			</Link>
			</Link>
			<Link title="BBD">
			</Link>
			</Link>
			<Link
				title="BC"
				icon="--menu-svg"
			>
			</Link>
			<Link title="BD">
			</Link>
			</Link>
			<Link
				title="C"
				icon="--close-svg"
			>
			</Link>
			<Link title="D">
			</Link>
		</Navigator>
	</Box>
</template>
<script>
	import Box from '@vueplayio/box';
	import Link from '@/components/Link.vue';
	import Navigator from '@/App.vue';
	export default {
		components: {
			Box: Box,
			Link: Link,
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