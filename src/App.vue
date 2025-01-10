<template>
	<div style="position:relative">
		<div>
			<Toggle
				icon="--menu-svg"
				:style="{
				width: iconSize
			}"
			/>
			<slot>
				Buttons comes here
			</slot>
		</div>
	</div>
</template>
<script>
	import Toggle from '@/components/Toggle.vue';
	export default {
		components: {
			Toggle: Toggle
		},
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
			}
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

</style>