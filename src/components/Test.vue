<template>
	<div :class="pathId"></div>
</template>
<script>
	export default {
		data: () => ({}),
		inject: ['pathId'],
		mounted() {
			console.log('pid', this.pathId);
		},
		watch: {
			pathId(id) {
				console.log('pid updated', id);
			}
		}
	};

</script>
<style scoped></style>