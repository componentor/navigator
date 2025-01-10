<template>
	<div
		:style="{
		'background-image': $icon
	}"
		style="background-size:contain;background-repeat:no-repeat;width:100%;aspect-ratio:1/1"
	>
	</div>
</template>
<script>
	export default {
		props: {
			icon: {
				type: String,
				control: 'media',
				default: '--vp-nav-default-icon'
			}
		},
		data: () => ({}),
		computed: {
			$icon() {
				if (this.icon?.startsWith('--')) {
					return `var(${this.icon})`;
				} else {
					return `url(${this.icon})`;
				}
			}
		}
	};

</script>
<style scoped>
	* {
		--vp-nav-default-icon: url(@/assets/menu.svg);
	}

</style>