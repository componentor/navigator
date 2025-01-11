<template>
	<div class="vp-navigator">
		<Toggle
			icon="--menu-svg"
			:style="{
				width: iconSize
			}"
			class="vp-toggle"
		/>
		<component
			:is="direction"
			class="vp-nav-items"
		>
			<slot>
				Drop Navigator Items Here
			</slot>
		</component>
	</div>
</template>
<script>
	import Column from '@vueplayio/column';
	import Row from '@vueplayio/row';
	import Toggle from '@/components/Toggle.vue';
	export default {
		props: {
			icon: {
				type: String,
				control: 'media',
				default: ''
			},
			iconSize: {
				type: String,
				control: 'slider',
				unit: 'px',
				default: '40px'
			},
			direction: {
				type: String,
				default: 'horizontal',
				options: [{
					key: 'Horizontal',
					value: 'Row'
				}, {
					key: 'Vertical',
					value: 'Column'
				}]
			}
		},
		components: {
			Column: Column,
			Row: Row,
			Toggle: Toggle
		},
		data: () => ({})
	};

</script>
<style></style>
<style scoped>
	* {
		--volleyball-svg: url(@/assets/volleyball.svg);
		--menu-svg: url(@/assets/menu.svg);
	}

	.vp-nav-items {
		display: inline-block;
	}

	.vp-toggle {
		display: none;
	}

</style>