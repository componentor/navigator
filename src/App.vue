<template>
	<div>
		<slot>
			<Button icon="--volleyball-svg"></Button><img
				src="@/assets/volleyball.svg"
				width="100"
				height="100"
			/>
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
			}
		},
		data: () => ({})
	};

</script>
<style></style>
<style scoped>
	* {
		--volleyball-svg: url(@/assets/volleyball.svg);
	}

</style>