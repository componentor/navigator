<template>
	<Row
		ref="navitem"
		:class="{ 'vp-navigator-item--small': small }"
		@mouseenter="show=true"
		@mouseleave="show=false"
		@click="show=true"
	>
		<template v-if="$slots.default && show">
			<div class="wrapper">
				<slot/>
			</div>
		</template>
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
				'background-image': $icon,
				'width': '40px'
			}"
			style="flex-shrink:0;background-size:contain;background-repeat:no-repeat;aspect-ratio:1/1"
		/>
		
	</Row>
</template>
<script>
	import { computed } from 'vue'
	import Row from '@vueplayio/row';
	export default {
		inject: ['small', 'open'],
		provide() {
			return {
				open: computed(() => this.show)
			}
		},
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
		components: {
			Row: Row
		},
		data: () => ({
			show: false
		}),
		mounted() {
			document.addEventListener('click', this.handleClickOutside)
		},
		beforeUnmount() {
			document.removeEventListener('click', this.handleClickOutside)
		},
		computed: {
			$icon() {
				if (this.icon?.startsWith('--')) {
					return `var(${this.icon})`;
				} else {
					return `url(${this.icon})`;
				}
			}
		},
		methods: {
			handleClickOutside(event) {
				if (this.show && this.$refs.navitem && !this.$refs.navitem.$el.contains(event.target)) {
					this.show = false
				}
			}
		}
	};

</script>
<style scoped>
	* {
		--vp-nav-default-icon: url(@/assets/menu.svg);
	}
	.vp-navigator-item--small {
		background: transparent
	}
</style>