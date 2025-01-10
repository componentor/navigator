<template>
	<router-link
		v-if="!external"
		:to="route"
		:target="target"
	>
		{{ title }}
	</router-link> <a
		v-else-if="external"
		:href="route"
		:target="target"
	>
		{{ title }}
	</a>
	<div
		:style="{
			'background-image': $icon
		}"
		style="background-size:contain;background-repeat:no-repeat;width:100%;aspect-ratio:1/1"
	/>
	<div>
		<slot>
			Slot
		</slot>
	</div>
</template>
<script>
	export default {
		props: {
			title: {
				type: String,
				default: 'Title'
			},
			route: {
				type: String
			},
			icon: {
				type: String,
				control: 'media',
				default: '--vp-nav-default-icon'
			},
			external: {
				type: Boolean,
				default: false
			},
			target: {
				type: String,
				default: ''
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