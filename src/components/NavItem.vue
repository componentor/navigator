<template>
	<component
		:is="horizontal ? 'Row' : 'Column'"
		:class="rootClass"
		:expand="expand"
		ref="navitem"
		class="vp-navigator-item"
		@mouseenter="horizontal ? show=true : ''"
		@mouseleave="horizontal ? show=false : ''"
		@click.stop="$slots.default && !route ? show=!show : ''"
	>
		<component
			v-if="icon"
			:is="external ? 'a' : 'router-link'"
			:to="route"
			:href="route"
			:target="target"
			class="vp-navigator-item--link"
			style="padding: 0 10px;display:flex;align-items:center"
		>
			<div
				:style="{
					'background-image': $icon,
					'width': $iconSize
				}"
				style="background-repeat:no-repeat;background-size:contain;background-position:center;aspect-ratio:1/1"
			/>
		</component>
		<component
			class="vp-navigator-item--link"
			:is="external ? 'a' : 'router-link'"
			:to="route"
			:href="route"
			:target="target"
			:style="{
				'flex-direction': (iconReverse === '' ? reverseIcon : (iconReverse === 'true')) ? 'row-reverse' : 'row',
				padding: '10px'
			}"
			style="white-space: nowrap;display:flex;align-items:center;flex-grow:1"
		>
			{{ title }}
		</component>
		<div
			v-if="$slots.default"
			@click.stop="show=!show"
			class="vp-navigator-item--link vp-navigator-item--arrow"
			style="padding: 0 10px;display:flex;align-items:center"
		>
			<div
				:style="{
					'background-image': $caret,
					'width': $caretSize
				}"
				style="background-repeat:no-repeat;background-size:contain;background-position:center;aspect-ratio:1/1"
			/>
		</div>
		<template v-if="$slots.default && (show || forceOpen || forceOpenProvider)">
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
		inject: [
			'small',
			'open',
			'forceOpenProvider',
			'direction',
			'orientation',
			'drop',
			'level',
			'order',
			'reverseIcon',
			'expand',
			'childrenIconSizeProvider',
			'childrenCaretProvider',
			'childrenCaretSizeProvider'
		],
		provide() {
			return {
				open: computed(() => this.show),
				forceOpenProvider: computed(() => this.forceOpen || this.forceOpenProvider),
				level: computed(() => this.level ? this.level + 1 : 1),
				order: computed(() => this.order === 'odd' ? 'even' : 'odd'),
				reverseIcon: computed(() => this.iconReverse === '' ? this.reverseIcon : (this.iconReverse === 'true')),
				childrenIconSizeProvider: computed(() => this.childrenIconSize || this.childrenIconSizeProvider),
				childrenCaretProvider: computed(() => this.childrenCaret || this.childrenCaretProvider),
				childrenCaretSizeProvider: computed(() => this.childrenCaretSize || this.childrenCaretSizeProvider),
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
			external: {
				type: Boolean,
				default: false
			},
			target: {
				type: String,
				default: ''
			},
			icon: {
				type: String,
				control: 'media',
				default: ''
			},
			iconSize: {
				type: String,
				default: '',
				control: 'slider'
			},
			childrenIconSize: {
				type: String,
				default: '',
				control: 'slider'
			},
			caret: {
				type: String,
				control: 'media',
				default: ''
			},
			caretSize: {
				type: String,
				default: '',
				control: 'slider'
			},
			childrenCaret: {
				type: String,
				control: 'media',
				default: ''
			},
			childrenCaretSize: {
				type: String,
				default: '',
				unit: 'px',
				control: 'slider'
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
			forceOpen: {
				type: Boolean,
				default: false
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
			$iconSize() {
				if (this.iconSize) return this.iconSize
				if (this.childrenIconSizeProvider) return this.childrenIconSizeProvider
				return '20px'
			},
			$icon() {
				if (this.icon?.startsWith('--')) {
					return `var(${this.icon})`;
				} else {
					return `url(${this.icon})`;
				}
			},
			$caret() {
				const caret = this.caret || this.childrenCaretProvider || '--vp-nav-caret-icon'
				if (caret?.startsWith('--')) {
					return `var(${caret})`;
				} else {
					return `url(${caret})`;
				}
			},
			$caretSize() {
				if (this.caretSize) return this.caretSize
				if (this.childrenCaretSizeProvider) return this.childrenCaretSizeProvider
				return '20px'
			},
			horizontal() {
				return this.orientation === 'Row'
			},
			rootClass() {
				const rootClass = {
					'vp-navigator-item--small': this.small,
					'vp-navigator-item--horizontal': this.horizontal,
					'vp-navigator-item--vertical': !this.horizontal,
					'vp-navigator-item--show': this.show,
					'vp-navigator-item--hide': !this.show,
					'vp-navigator-item--direction-left': this.direction === 'left',
					'vp-navigator-item--drop-up': this.drop === 'up',
					'vp-navigator-item--reverse': (this.iconReverse === '' ? this.reverseIcon : (this.iconReverse === 'true'))
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
		--vp-nav-caret-icon: url(@/assets/arrow.svg);
	}
	.vp-navigator-item {
		position: relative;
		background: 'inherit';
		overflow: visible;
		padding: 0;
		cursor: pointer;
		border-bottom: 1px solid black;
		align-items: stretch;
	}
	.vp-navigator-item:hover {
		background-color: rgb(0, 0, 0, 0.1)
	}
	.vp-navigator-item--small {
		background: transparent;
	}
	.vp-navigator-item--drop-up {
		background: transparent;
	}
	.vp-navigator-item--vertical.vp-navigator-item--show .vp-navigator-item--arrow {
		transform: rotate(90deg);
	}
	.vp-navigator-item--vertical.vp-navigator-item--hide .vp-navigator-item--arrow {
		transform: rotate(0deg);
	}
	.vp-navigator-item--reverse.vp-navigator-item--vertical.vp-navigator-item--hide .vp-navigator-item--arrow {
		transform: rotate(-180deg);
	}
	.vp-navigator-item--horizontal.vp-navigator-item--level-0 .vp-navigator-item--arrow {
		transform: rotate(90deg);
	}
	.vp-navigator-item--reverse.vp-navigator-item--horizontal.vp-navigator-item--level-0 .vp-navigator-item--arrow {
		transform: rotate(90deg);
	}
	.vp-navigator-item--horizontal.vp-navigator-item--level-1 .vp-navigator-item--arrow {
		transform: rotate(0deg);
	}
	.vp-navigator-item--reverse.vp-navigator-item--horizontal.vp-navigator-item--level-1 .vp-navigator-item--arrow {
		transform: rotate(-180deg);
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
	.vp-navigator-item--direction-left.vp-navigator-item--horizontal:not(.vp-navigator-item--level-0) .wrapper {
		left: auto;
		right: 100%;
	}
	.vp-navigator-item:not(.vp-navigator-item--level-0) {
	}
	.vp-navigator-item--odd {
		background: 'inherit'
	}
	.vp-navigator-item--even {
		background: 'inherit'
	}
	.vp-navigator-item--link {
		background: 'inherit'
	}
	.vp-navigator-item--reverse {
	}
</style>