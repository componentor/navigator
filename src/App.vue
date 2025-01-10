<template>
	<div>
		<slot>
			<Button icon="url(@/assets/volleyball.svg)"></Button>
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