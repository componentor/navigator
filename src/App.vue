<template>
	<div>
		<Button
			icon="--menu-svg"
			:style="{
				width: iconSize
			}"
		/>
		<slot>
			Buttons comes here
		</slot>
	</div>
</template>
<script>
	import Button from '@/components/Button.vue';
	export default {
		components: {
			Button: Button
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