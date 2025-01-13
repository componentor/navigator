<template>
	<div
		v-if="!open"
		:style="{
			'background-image': $icon
		}"
		style="cursor:pointer;background-size:contain;background-repeat:no-repeat;width:100%;aspect-ratio:1/1"
	/>
	<div
		v-else-if="open"
		:style="{
			'background-image': $iconClose
		}"
		style="cursor:pointer;background-size:contain;background-repeat:no-repeat;width:100%;aspect-ratio:1/1"
	/>
</template>
<script>
	export default {
		props: {
			open: {
				type: Boolean,
				default: false
			},
			icon: {
				type: String,
				control: 'media',
				default: '--vp-nav-default-icon'
			},
			iconClose: {
				type: String,
				control: 'media',
				default: '--vp-nav-default-icon-close'
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
			},
			$iconClose() {
				if (this.iconClose?.startsWith('--')) {
					return `var(${this.iconClose})`;
				} else {
					return `url(${this.iconClose})`;
				}
			}
		}
	};

</script>
<style scoped>
	* {
		--vp-nav-default-icon: url(@/assets/menu.svg);
		--vp-nav-default-icon-close: url(@/assets/close.svg);
	}

</style>