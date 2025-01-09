<template>
	<div>
		<slot><Button></Button></slot>
	</div>
</template>
<script>
	import Button from '@/components/Button.vue';
	export default {
		components: {
			Button: Button
		},
		data: () => ({})
	};

</script>
<style></style>