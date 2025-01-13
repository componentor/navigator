<template>
	<component
		:is="horizontal ? 'Row' : 'Column'"
		:class="rootClass"
		:reverse="iconReverse === '' ? reverseIcon : (iconReverse === 'true')"
		:expand="expand"
		ref="navitem"
		class="vp-navigator-item"
		style="padding: 0"
		@mouseenter="horizontal ? show=true : ''"
		@mouseleave="horizontal ? show=false : ''"
		@click.stop="show=!show"
	>
		<component
			:is="external ? 'a' : 'router-link'"
			:to="route"
			:href="route"
			:target="target"
			:style="{
				padding: '10px'
			}"
			style="display:flex;justify-content: space-between; border-bottom: 1px solid blue;align-items:center"
		>
			<div
				:style="{
					'background-image': $icon,
					'width': '20px'
				}"
				style="flex-shrink:0;background-size:contain;background-repeat:no-repeat;aspect-ratio:1/1"
			/>
			{{ title }}
		</component>
		<template v-if="$slots.default && show">
			<div class="wrapper">
				<slot/>
			</div>
		</template>
	</component>
</template>
<script>
	import { computed } from 'vue'
	import Row from '@vueplayio/row';
	import Column from '@vueplayio/column';
	export default {
		inject: ['small', 'open', 'direction', 'level', 'order', 'reverseIcon'],
		provide() {
			return {
				open: computed(() => this.show),
				level: this.level ? this.level + 1 : 1,
				order: this.order === 'odd' ? 'even' : 'odd',
				reverseIcon: computed(() => this.iconReverse === '' ? this.reverseIcon : (this.iconReverse === 'true'))
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
			iconReverse: {
				type: String,
				default: '',
				options: [
					{ key: 'Default', value: '' },
					{ key: 'Yes', value: 'true' },
					{ key: 'No', value: 'false' },
				]
			},
			expand: {
				type: Boolean,
				default: null
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
			Row: Row,
			Column: Column
		},
		data: () => ({
			show: false
		}),
		mounted() {
			if (this.horizontal) {
				document.addEventListener('click', this.handleClickOutside)
			}
		},
		beforeUnmount() {
			if (this.horizontal) {
				document.removeEventListener('click', this.handleClickOutside)
			}
		},
		watch: {
			horizontal(horizontal) {
				if (horizontal) {
					document.addEventListener('click', this.handleClickOutside)
				} else {
					document.removeEventListener('click', this.handleClickOutside)
				}
			}
		},
		computed: {
			$icon() {
				if (this.icon?.startsWith('--')) {
					return `var(${this.icon})`;
				} else {
					return `url(${this.icon})`;
				}
			},
			horizontal() {
				return this.direction === 'Row'
			},
			rootClass() {
				const rootClass = {
					'vp-navigator-item--small': this.small,
					'vp-navigator-item--horizontal': this.horizontal,
				}
				const level = this.level || 0
				rootClass[`vp-navigator-item--level-${level}`] = true
				rootClass[`vp-navigator-item--${this.order}`] = true
				return rootClass
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
	.vp-navigator-item {
		position: relative;
		background: rgb(200, 0, 0, 0.1);
		overflow: visible
	}
	.vp-navigator-item--small {
		background: transparent;
	}
	.vp-navigator-item--level-0 {
		background: yellow
	}
	.vp-navigator-item--horizontal.vp-navigator-item--level-0 .wrapper {
		position: absolute;
		top: 100%;
	}
	.vp-navigator-item--horizontal:not(.vp-navigator-item--level-0) .wrapper {
		position: absolute;
		top: 0%;
		left: 100%;
	}
	.vp-navigator-item--odd {
		background: yellow
	}
	.vp-navigator-item--even {
		background: yellow
	}
</style>