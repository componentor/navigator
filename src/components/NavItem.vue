<template>
	<template v-if="drop === 'up' && order !== 'odd' && $vertical && $slots.default && (show || forceOpen || forceOpenProvider)">
		<div class="wrapper vp-navigator-item--up">
			<slot />
		</div>
	</template>
	<Row
		v-bind="$attrs"
		:class="rootClass"
		:expand="expand"
		:style="{
			'flex-direction': (iconReverse === '' ? reverseIcon : (iconReverse === 'true')) ? 'row-reverse' : 'row',
		}"
		ref="navitem"
		class="vp-navigator-item"
		@click.stop="($event.pointerType !== 'mouse' || $vertical) && $slots.default && !route ? show=!show : ''"
		@pointerover="$event.pointerType !== 'mouse' || $vertical ? '' : show=true"
		@pointerleave="$event.pointerType !== 'mouse' || $vertical ? '' : show=false"
	>
		<component
			v-if="icon"
			:is="external ? 'a' : 'router-link'"
			:to="route"
			:href="route"
			:target="target"
			class="vp-navigator-item--link"
			style="padding: 0 10px;display:inline-flex;align-items:center"
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
				padding: '10px'
			}"
			style="white-space: nowrap;display:inline-flex;align-items:center;flex-grow:1"
		>
			{{ title }}
		</component>
		<div
			v-if="$slots.default"
			@click.stop="show=!show"
			class="vp-navigator-item--link vp-navigator-item--arrow"
			style="padding: 0 10px;display:inline-flex;align-items:center"
		>
			<div
				:style="{
					'background-image': $caret,
					'width': $caretSize
				}"
				style="background-repeat:no-repeat;background-size:contain;background-position:center;aspect-ratio:1/1"
			/>
		</div> <template v-if="!$vertical && $slots.default && (show || forceOpen || forceOpenProvider)">
			<div class="wrapper">
				<slot />
			</div>
		</template>
	</Row> <template v-if="(drop !== 'up' || order === 'odd') && $vertical && $slots.default && (show || forceOpen || forceOpenProvider)">
		<div class="wrapper">
			<slot />
		</div>
	</template>
</template>
<script>
	import {
		computed
	} from 'vue';
	import Row from '@vueplayio/row';
	export default {
		inject: ['small', 'open', 'forceOpenProvider', 'direction', 'orientation', 'drop', 'level', 'order', 'reverseIcon', 'expand', 'childrenIconSizeProvider', 'childrenCaretProvider', 'childrenCaretSizeProvider'],
		provide() {
			return {
				open: computed(() => this.show),
				forceOpenProvider: computed(() => this.forceOpen || this.forceOpenProvider),
				level: computed(() => this.level ? this.level + 1 : 1),
				order: computed(() => this.order === 'odd' ? 'even' : 'odd'),
				reverseIcon: computed(() => this.iconReverse === '' ? this.reverseIcon : this.iconReverse === 'true'),
				childrenIconSizeProvider: computed(() => this.childrenIconSize || this.childrenIconSizeProvider),
				childrenCaretProvider: computed(() => this.childrenCaret || this.childrenCaretProvider),
				childrenCaretSizeProvider: computed(() => this.childrenCaretSize || this.childrenCaretSizeProvider),
				direction: computed(() => this.itemDirection || this.direction)
			};
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
				options: [{
					key: 'Default',
					value: ''
				}, {
					key: 'Yes',
					value: 'true'
				}, {
					key: 'No',
					value: 'false'
				}]
			},
			itemDirection: {
				type: String,
				default: '',
				options: [{
					key: 'Default',
					value: ''
				}, {
					key: 'Left',
					value: 'left'
				}, {
					key: 'Right',
					value: 'right'
				}]
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
			Row: Row
		},
		data: () => ({
			show: false
		}),
		mounted() {
			document.addEventListener('click', this.handleClickOutside);
		},
		beforeUnmount() {
			document.removeEventListener('click', this.handleClickOutside);
		},
		computed: {
			$vertical() {
				return !this.horizontal || this.small;
			},
			$iconSize() {
				if (this.iconSize) return this.iconSize;
				if (this.childrenIconSizeProvider) return this.childrenIconSizeProvider;
				return '20px';
			},
			$icon() {
				if (this.icon?.startsWith('--')) {
					return `var(${this.icon})`;
				} else {
					return `url(${this.icon})`;
				}
			},
			$caret() {
				const caret = this.caret || this.childrenCaretProvider || '--vp-nav-caret-icon';
				if (caret?.startsWith('--')) {
					return `var(${caret})`;
				} else {
					return `url(${caret})`;
				}
			},
			$caretSize() {
				if (this.caretSize) return this.caretSize;
				if (this.childrenCaretSizeProvider) return this.childrenCaretSizeProvider;
				return '20px';
			},
			horizontal() {
				return this.orientation === 'Row';
			},
			rootClass() {
				const rootClass = {
					'vp-navigator-item--small': this.small,
					'vp-navigator-item--horizontal': !this.$vertical,
					'vp-navigator-item--vertical': this.$vertical,
					'vp-navigator-item--show': this.show || this.forceOpen || this.forceOpenProvider,
					'vp-navigator-item--hide': !this.show && !this.forceOpen && !this.forceOpenProvider,
					'vp-navigator-item--direction-left': this.itemDirection ? this.itemDirection === 'left' : this.direction === 'left',
					'vp-navigator-item--direction-right': this.itemDirection ? this.itemDirection === 'right' : this.direction === 'right',
					'vp-navigator-item--drop-up': this.drop === 'up',
					'vp-navigator-item--reverse': this.iconReverse === '' ? this.reverseIcon : this.iconReverse === 'true'
				};
				const level = this.level || 0;
				rootClass[`vp-navigator-item--level-${level}`] = true;
				rootClass[`vp-navigator-item--${this.order}`] = true;
				return rootClass;
			}
		},
		methods: {
			handleClickOutside(event) {
				if (this.show && this.$refs.navitem && !this.$refs.navitem.$el.contains(event.target)) {
					this.show = false;
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
		background-color: rgb(0, 0, 0, 0.1);
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

	.vp-navigator-item--drop-up.vp-navigator-item--vertical.vp-navigator-item--show .vp-navigator-item--arrow {
		transform: rotate(-90deg);
	}

	.vp-navigator-item--vertical.vp-navigator-item--hide .vp-navigator-item--arrow,
	.vp-navigator-item--drop-up.vp-navigator-item--vertical.vp-navigator-item--hide .vp-navigator-item--arrow {
		transform: rotate(0deg);
	}

	.vp-navigator-item--reverse.vp-navigator-item--vertical.vp-navigator-item--hide .vp-navigator-item--arrow,
	.vp-navigator-item--drop-up.vp-navigator-item--reverse.vp-navigator-item--vertical.vp-navigator-item--hide .vp-navigator-item--arrow {
		transform: rotate(-180deg);
	}

	.vp-navigator-item--horizontal.vp-navigator-item--level-0 .vp-navigator-item--arrow,
	.vp-navigator-item--reverse.vp-navigator-item--horizontal.vp-navigator-item--level-0 .vp-navigator-item--arrow {
		transform: rotate(90deg);
	}

	.vp-navigator-item--drop-up.vp-navigator-item--horizontal.vp-navigator-item--level-0 .vp-navigator-item--arrow,
	.vp-navigator-item--drop-up.vp-navigator-item--reverse.vp-navigator-item--horizontal.vp-navigator-item--level-0 .vp-navigator-item--arrow {
		transform: rotate(-90deg);
	}

	.vp-navigator-item--horizontal.vp-navigator-item--level-1 .vp-navigator-item--arrow,
	.vp-navigator-item--drop-up.vp-navigator-item--horizontal.vp-navigator-item--level-1 .vp-navigator-item--arrow {
		transform: rotate(0deg);
	}

	.vp-navigator-item--reverse.vp-navigator-item--horizontal.vp-navigator-item--level-1 .vp-navigator-item--arrow,
	.vp-navigator-item--drop-up.vp-navigator-item--reverse.vp-navigator-item--horizontal.vp-navigator-item--level-1 .vp-navigator-item--arrow {
		transform: rotate(0deg);
	}

	.vp-navigator-item--direction-left.vp-navigator-item--horizontal.vp-navigator-item--level-1 .vp-navigator-item--arrow,
	.vp-navigator-item--direction-left.vp-navigator-item--reverse.vp-navigator-item--horizontal.vp-navigator-item--level-1 .vp-navigator-item--arrow,
	.vp-navigator-item--direction-left.vp-navigator-item--drop-up.vp-navigator-item--reverse.vp-navigator-item--horizontal.vp-navigator-item--level-1 .vp-navigator-item--arrow {
		transform: rotate(-180deg);
	}

	.vp-navigator-item--direction-right.vp-navigator-item--horizontal.vp-navigator-item--level-1 .vp-navigator-item--arrow,
	.vp-navigator-item--direction-right.vp-navigator-item--reverse.vp-navigator-item--horizontal.vp-navigator-item--level-1 .vp-navigator-item--arrow,
	.vp-navigator-item--direction-right.vp-navigator-item--drop-up.vp-navigator-item--reverse.vp-navigator-item--horizontal.vp-navigator-item--level-1 .vp-navigator-item--arrow {
		transform: rotate(0deg);
	}

	.vp-navigator-item--horizontal.vp-navigator-item--level-0 .wrapper {
		position: absolute;
		min-width: 100%;
		top: 100%;
	}

	.vp-navigator-item--drop-up.vp-navigator-item--horizontal.vp-navigator-item--level-0 .wrapper {
		position: absolute;
		min-width: 100%;
		top: auto;
		bottom: 100%;
	}

	.vp-navigator-item--up.wrapper {
		display: flex;
		flex-direction: column-reverse;
	}

	.vp-navigator-item--horizontal:not(.vp-navigator-item--level-0) .wrapper {
		position: absolute;
		top: 0%;
		left: 100%;
	}

	.vp-navigator-item--drop-up.vp-navigator-item--horizontal:not(.vp-navigator-item--level-0) .wrapper {
		position: absolute;
		bottom: 0%;
		left: 100%;
	}

	.vp-navigator-item--direction-left.vp-navigator-item--horizontal:not(.vp-navigator-item--level-0) .wrapper {
		left: auto;
		right: 100%;
	}

	.vp-navigator-item--direction-right.vp-navigator-item--horizontal:not(.vp-navigator-item--level-0) .wrapper {
		left: 100%;
		right: auto;
	}

	.vp-navigator-item--odd {
		background: 'inherit';
	}

	.vp-navigator-item--even {
		background: 'inherit';
	}

	.vp-navigator-item--link {
		background: 'inherit';
	}

</style>