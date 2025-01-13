<template>
	<component
		:is="horizontal ? 'Row' : 'Column'"
		:class="rootClass"
		:expand="expand"
		ref="navitem"
		class="vp-navigator-item"
		style="padding: 0;cursor:pointer"
		@mouseenter="horizontal ? show=true : ''"
		@mouseleave="horizontal ? show=false : ''"
		@click.stop="$slots.default && !route ? show=!show : ''"
	>
		<component
			class="vp-navigator-item--link"
			:is="external ? 'a' : 'router-link'"
			:to="route"
			:href="route"
			:target="target"
			:style="{
				'flex-direction': (iconReverse === '' ? reverseIcon : (iconReverse === 'true')) ? 'row-reverse' : 'row'
			}"
			style="flex-grow: 1;display:flex;justify-content: space-between; align-items:center"
		>
			<div
				v-if="icon"
				:style="{
					'background-image': $icon,
					'background-size': '50%',
					'background-position': 'center',
					'height': $slots.default ? '40px' : '0px',
				}"
				style="position:relative;flex-shrink:0;background-repeat:no-repeat;aspect-ratio:1/1"
			/>
			<div style="justify-content: space-between;flex-grow: 1;display:flex;">
				<div style="display: flex;padding: 10px">
					{{ title }}
				</div>
				<div
					@click.stop="show=!show"
					class="vp-navigator-item--arrow"
					:style="{
						'background-size': '50%',
						'background-position': 'center',
						'background-image': 'var(--vp-nav-arrow-icon)',
						'height': $slots.default ? '40px' : '0px',
					}"
					style="display: flex;cursor: pointer; background-repeat:no-repeat;aspect-ratio:1/1"
				/>
			</div>
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
				default: ''
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
					'vp-navigator-item--vertical': !this.horizontal,
					'vp-navigator-item--show': this.show,
					'vp-navigator-item--hide': !this.show,
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
		--vp-nav-arrow-icon: url(@/assets/arrow.svg);
	}
	.vp-navigator-item {
		position: relative;
		background: 'inherit';
		overflow: visible
	}
	.vp-navigator-item--small {
		background: transparent;
	}
	.vp-navigator-item--vertical.vp-navigator-item--show .vp-navigator-item--arrow {
		transform: rotate(90deg);
	}
	.vp-navigator-item--vertical.vp-navigator-item--hide .vp-navigator-item--arrow {
		transform: rotate(0deg);
	}
	.vp-navigator-item--horizontal.vp-navigator-item--level-0 .vp-navigator-item--arrow {
		transform: rotate(90deg);
	}
	.vp-navigator-item--horizontal.vp-navigator-item--level-1 .vp-navigator-item--arrow {
		transform: rotate(0deg);
	}
	.vp-navigator-item--horizontal.vp-navigator-item--level-0 .wrapper {
		position: absolute;
		min-width: 100%;
		top: 100%;
	}
	.vp-navigator-item--horizontal:not(.vp-navigator-item--level-0) .wrapper {
		position: absolute;
		top: 0%;
		left: 100%;
	}
	.vp-navigator-item--odd {
		background: 'inherit'
	}
	.vp-navigator-item--even {
		background: 'inherit'
	}
	.vp-navigator-item--link {
		border-bottom: 1px solid black;
	}
	.vp-navigator-item--link:hover {
		background-color: rgb(0, 0, 0, 0.1)
	}
</style>