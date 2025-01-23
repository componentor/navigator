<template>
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
		</div> <template v-if="!$vertical">
			<div v-show="$slots.default && (show || forceOpen || forceOpenProvider)" class="wrapper" :class="{
				'vp-navigator-item--up': drop === 'up'
			}" :style="{ 'z-index': level ? level + 1 : 1 }">
				<slot />
			</div>
		</template>
	</Row>
	<template v-if="$vertical">
		<div v-if="$slots.default && (show || forceOpen || forceOpenProvider)" class="wrapper" :class="{
			'vp-navigator-item--up': drop === 'up'
		}">
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
		inject: ['small', 'open', 'forceOpenProvider', 'direction', 'orientation', 'drop', 'level', 'order', 'reverseIcon', 'expand', 'childrenIconSizeProvider', 'childrenCaretProvider', 'childrenCaretSizeProvider', 'model'],
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
				direction: computed(() => this.itemDirection ? this.itemDirection : this.direction),
				model: computed(() => this.childModel)
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
				default: '',
				options: [{
					key: 'Default',
					value: ''
				}, {
					key: 'Blank',
					value: '_blank'
				}, {
					key: 'Self',
					value: '_self'
				}, {
					key: 'Parent',
					value: '_parent'
				}, {
					key: 'Top',
					value: '_top'
				}]
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
			},
			textColor: {
				type: String,
				default: '',
				control: 'color',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			backgroundColor: {
				type: String,
				default: '',
				control: 'color',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			backgroundImage: {
				type: String,
				default: '',
				control: 'media',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderTopColor: {
				type: String,
				default: '',
				control: 'color',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderRightColor: {
				type: String,
				default: '',
				control: 'color',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderBottomColor: {
				type: String,
				default: '',
				control: 'color',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderLeftColor: {
				type: String,
				default: '',
				control: 'color',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderTopWidth: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderRightWidth: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderBottomWidth: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderLeftWidth: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderTopStyle: {
				type: String,
				default: '',
				options: [
					{ value: '', key: 'Clear' },
					{ value: 'none', key: 'none' },
					{ value: 'hidden', key: 'hidden' },
					{ value: 'solid', key: 'solid' },
					{ value: 'dashed', key: 'dashed' },
					{ value: 'dotted', key: 'dotted' },
					{ value: 'double', key: 'double' },
					{ value: 'groove', key: 'groove' },
					{ value: 'ridge', key: 'ridge' },
					{ value: 'inset', key: 'inset' },
					{ value: 'outset', key: 'outset' }
				],
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderRightStyle: {
				type: String,
				default: '',
				options: [
					{ value: '', key: 'Clear' },
					{ value: 'none', key: 'none' },
					{ value: 'hidden', key: 'hidden' },
					{ value: 'solid', key: 'solid' },
					{ value: 'dashed', key: 'dashed' },
					{ value: 'dotted', key: 'dotted' },
					{ value: 'double', key: 'double' },
					{ value: 'groove', key: 'groove' },
					{ value: 'ridge', key: 'ridge' },
					{ value: 'inset', key: 'inset' },
					{ value: 'outset', key: 'outset' }
				],
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderBottomStyle: {
				type: String,
				default: '',
				options: [
					{ value: '', key: 'Clear' },
					{ value: 'none', key: 'none' },
					{ value: 'hidden', key: 'hidden' },
					{ value: 'solid', key: 'solid' },
					{ value: 'dashed', key: 'dashed' },
					{ value: 'dotted', key: 'dotted' },
					{ value: 'double', key: 'double' },
					{ value: 'groove', key: 'groove' },
					{ value: 'ridge', key: 'ridge' },
					{ value: 'inset', key: 'inset' },
					{ value: 'outset', key: 'outset' }
				],
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderLeftStyle: {
				type: String,
				default: '',
				options: [
					{ value: '', key: 'Clear' },
					{ value: 'none', key: 'none' },
					{ value: 'hidden', key: 'hidden' },
					{ value: 'solid', key: 'solid' },
					{ value: 'dashed', key: 'dashed' },
					{ value: 'dotted', key: 'dotted' },
					{ value: 'double', key: 'double' },
					{ value: 'groove', key: 'groove' },
					{ value: 'ridge', key: 'ridge' },
					{ value: 'inset', key: 'inset' },
					{ value: 'outset', key: 'outset' }
				],
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderTopLeftRadius: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderTopRightRadius: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderBottomRightRadius: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderBottomLeftRadius: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			paddingTop: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			paddingRight: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			paddingBottom: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			paddingLeft: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			marginTop: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			marginRight: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			marginBottom: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			marginLeft: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			}
		},
		components: {
			Row: Row
		},
		data: () => ({
			show: false,
			childModel: {}
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
			},
			selfModel() {
				const def = 'ignore'
				const defaultValues = {
					xs: { light: def, dark: def },
					sm: { light: def, dark: def },
					md: { light: def, dark: def },
					lg: { light: def, dark: def },
					xl: { light: def, dark: def },
					'2xl': { light: def, dark: def },
				};

				const props = [
					'textColor',
					'backgroundColor',
					'backgroundImage',
					'borderTopColor',
					'borderRightColor',
					'borderBottomColor',
					'borderLeftColor',
					'borderTopWidth',
					'borderRightWidth',
					'borderBottomWidth',
					'borderLeftWidth',
					'borderTopStyle',
					'borderRightStyle',
					'borderBottomStyle',
					'borderLeftStyle',
					'borderTopLeftRadius',
					'borderTopRightRadius',
					'borderBottomRightRadius',
					'borderBottomLeftRadius',
					'paddingTop',
					'paddingRight',
					'paddingBottom',
					'paddingLeft',
					'marginTop',
					'marginRight',
					'marginBottom',
					'marginLeft',
				];

				const defaultStyle = {
					default: { ...defaultValues },
					hover: { ...defaultValues },
					current: { ...defaultValues },
					active: { ...defaultValues },
					focus: { ...defaultValues },
				}

				const defaultStyleString = JSON.stringify(defaultStyle)

				const obj = {}

				this.childModel = {}
				for (const prop of props) {
					obj[prop] = defaultStyle
					const parsedValue = this[prop]
						? JSON.parse(this[prop].replaceAll('`', '"')) 
						: this.model?.[prop];
					if (parsedValue) {
						obj[prop] = JSON.parse(defaultStyleString)
						this.childModel[prop] = parsedValue
						for (const group in parsedValue) {
							for (const breakpoint in parsedValue[group]) {
								for (const theme in parsedValue[group][breakpoint]) {
									if (parsedValue[group][breakpoint][theme]) {
										obj[prop][group][breakpoint][theme] = parsedValue[group][breakpoint][theme];
									}
								}
							}
						}
					}
				}

				return obj;
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
		overflow: visible;
		padding: 0;
		cursor: pointer;
		border-bottom: 1px solid black;
		align-items: stretch;
	}

	.vp-navigator-item {
		color: v-bind(selfModel.textColor.default.xs.light);
		background-color: v-bind(selfModel.backgroundColor.default.xs.light);
		background-image: v-bind(selfModel.backgroundImage.default.xs.light);
		border-top-color: v-bind(selfModel.borderTopColor.default.xs.light);
		border-right-color: v-bind(selfModel.borderRightColor.default.xs.light);
		border-bottom-color: v-bind(selfModel.borderBottomColor.default.xs.light);
		border-left-color: v-bind(selfModel.borderLeftColor.default.xs.light);
		border-top-width: v-bind(selfModel.borderTopWidth.default.xs.light);
		border-right-width: v-bind(selfModel.borderRightWidth.default.xs.light);
		border-bottom-width: v-bind(selfModel.borderBottomWidth.default.xs.light);
		border-left-width: v-bind(selfModel.borderLeftWidth.default.xs.light);
		border-top-style: v-bind(selfModel.borderTopStyle.default.xs.light);
		border-right-style: v-bind(selfModel.borderRightStyle.default.xs.light);
		border-bottom-style: v-bind(selfModel.borderBottomStyle.default.xs.light);
		border-left-style: v-bind(selfModel.borderLeftStyle.default.xs.light);
		border-top-left-radius: v-bind(selfModel.borderTopLeftRadius.default.xs.light);
		border-top-right-radius: v-bind(selfModel.borderTopRightRadius.default.xs.light);
		border-bottom-right-radius: v-bind(selfModel.borderBottomRightRadius.default.xs.light);
		border-bottom-left-radius: v-bind(selfModel.borderBottomLeftRadius.default.xs.light);
		padding-top: v-bind(selfModel.paddingTop.default.xs.light);
		padding-right: v-bind(selfModel.paddingRight.default.xs.light);
		padding-bottom: v-bind(selfModel.paddingBottom.default.xs.light);
		padding-left: v-bind(selfModel.paddingLeft.default.xs.light);
		margin-top: v-bind(selfModel.marginTop.default.xs.light);
		margin-right: v-bind(selfModel.marginRight.default.xs.light);
		margin-bottom: v-bind(selfModel.marginBottom.default.xs.light);
		margin-left: v-bind(selfModel.marginLeft.default.xs.light);
	}

	.vp-navigator-item:hover {
		color: v-bind(selfModel.textColor.hover.xs.light);
		background-color: v-bind(selfModel.backgroundColor.hover.xs.light);
		background-image: v-bind(selfModel.backgroundImage.hover.xs.light);
		border-top-color: v-bind(selfModel.borderTopColor.hover.xs.light);
		border-right-color: v-bind(selfModel.borderRightColor.hover.xs.light);
		border-bottom-color: v-bind(selfModel.borderBottomColor.hover.xs.light);
		border-left-color: v-bind(selfModel.borderLeftColor.hover.xs.light);
		border-top-width: v-bind(selfModel.borderTopWidth.hover.xs.light);
		border-right-width: v-bind(selfModel.borderRightWidth.hover.xs.light);
		border-bottom-width: v-bind(selfModel.borderBottomWidth.hover.xs.light);
		border-left-width: v-bind(selfModel.borderLeftWidth.hover.xs.light);
		border-top-style: v-bind(selfModel.borderTopStyle.hover.xs.light);
		border-right-style: v-bind(selfModel.borderRightStyle.hover.xs.light);
		border-bottom-style: v-bind(selfModel.borderBottomStyle.hover.xs.light);
		border-left-style: v-bind(selfModel.borderLeftStyle.hover.xs.light);
		border-top-left-radius: v-bind(selfModel.borderTopLeftRadius.hover.xs.light);
		border-top-right-radius: v-bind(selfModel.borderTopRightRadius.hover.xs.light);
		border-bottom-right-radius: v-bind(selfModel.borderBottomRightRadius.hover.xs.light);
		border-bottom-left-radius: v-bind(selfModel.borderBottomLeftRadius.hover.xs.light);
		padding-top: v-bind(selfModel.paddingTop.hover.xs.light);
		padding-right: v-bind(selfModel.paddingRight.hover.xs.light);
		padding-bottom: v-bind(selfModel.paddingBottom.hover.xs.light);
		padding-left: v-bind(selfModel.paddingLeft.hover.xs.light);
		margin-top: v-bind(selfModel.marginTop.hover.xs.light);
		margin-right: v-bind(selfModel.marginRight.hover.xs.light);
		margin-bottom: v-bind(selfModel.marginBottom.hover.xs.light);
		margin-left: v-bind(selfModel.marginLeft.hover.xs.light);
	}

	.vp-navigator-item.current {
		color: v-bind(selfModel.textColor.current.xs.light);
		background-color: v-bind(selfModel.backgroundColor.current.xs.light);
		background-image: v-bind(selfModel.backgroundImage.current.xs.light);
		border-top-color: v-bind(selfModel.borderTopColor.current.xs.light);
		border-right-color: v-bind(selfModel.borderRightColor.current.xs.light);
		border-bottom-color: v-bind(selfModel.borderBottomColor.current.xs.light);
		border-left-color: v-bind(selfModel.borderLeftColor.current.xs.light);
		border-top-width: v-bind(selfModel.borderTopWidth.current.xs.light);
		border-right-width: v-bind(selfModel.borderRightWidth.current.xs.light);
		border-bottom-width: v-bind(selfModel.borderBottomWidth.current.xs.light);
		border-left-width: v-bind(selfModel.borderLeftWidth.current.xs.light);
		border-top-style: v-bind(selfModel.borderTopStyle.current.xs.light);
		border-right-style: v-bind(selfModel.borderRightStyle.current.xs.light);
		border-bottom-style: v-bind(selfModel.borderBottomStyle.current.xs.light);
		border-left-style: v-bind(selfModel.borderLeftStyle.current.xs.light);
		border-top-left-radius: v-bind(selfModel.borderTopLeftRadius.current.xs.light);
		border-top-right-radius: v-bind(selfModel.borderTopRightRadius.current.xs.light);
		border-bottom-right-radius: v-bind(selfModel.borderBottomRightRadius.current.xs.light);
		border-bottom-left-radius: v-bind(selfModel.borderBottomLeftRadius.current.xs.light);
		padding-top: v-bind(selfModel.paddingTop.current.xs.light);
		padding-right: v-bind(selfModel.paddingRight.current.xs.light);
		padding-bottom: v-bind(selfModel.paddingBottom.current.xs.light);
		padding-left: v-bind(selfModel.paddingLeft.current.xs.light);
		margin-top: v-bind(selfModel.marginTop.current.xs.light);
		margin-right: v-bind(selfModel.marginRight.current.xs.light);
		margin-bottom: v-bind(selfModel.marginBottom.current.xs.light);
		margin-left: v-bind(selfModel.marginLeft.current.xs.light);
	}

	.vp-navigator-item:active {
		color: v-bind(selfModel.textColor.active.xs.light);
		background-color: v-bind(selfModel.backgroundColor.active.xs.light);
		background-image: v-bind(selfModel.backgroundImage.active.xs.light);
		border-top-color: v-bind(selfModel.borderTopColor.active.xs.light);
		border-right-color: v-bind(selfModel.borderRightColor.active.xs.light);
		border-bottom-color: v-bind(selfModel.borderBottomColor.active.xs.light);
		border-left-color: v-bind(selfModel.borderLeftColor.active.xs.light);
		border-top-width: v-bind(selfModel.borderTopWidth.active.xs.light);
		border-right-width: v-bind(selfModel.borderRightWidth.active.xs.light);
		border-bottom-width: v-bind(selfModel.borderBottomWidth.active.xs.light);
		border-left-width: v-bind(selfModel.borderLeftWidth.active.xs.light);
		border-top-style: v-bind(selfModel.borderTopStyle.active.xs.light);
		border-right-style: v-bind(selfModel.borderRightStyle.active.xs.light);
		border-bottom-style: v-bind(selfModel.borderBottomStyle.active.xs.light);
		border-left-style: v-bind(selfModel.borderLeftStyle.active.xs.light);
		border-top-left-radius: v-bind(selfModel.borderTopLeftRadius.active.xs.light);
		border-top-right-radius: v-bind(selfModel.borderTopRightRadius.active.xs.light);
		border-bottom-right-radius: v-bind(selfModel.borderBottomRightRadius.active.xs.light);
		border-bottom-left-radius: v-bind(selfModel.borderBottomLeftRadius.active.xs.light);
		padding-top: v-bind(selfModel.paddingTop.active.xs.light);
		padding-right: v-bind(selfModel.paddingRight.active.xs.light);
		padding-bottom: v-bind(selfModel.paddingBottom.active.xs.light);
		padding-left: v-bind(selfModel.paddingLeft.active.xs.light);
		margin-top: v-bind(selfModel.marginTop.active.xs.light);
		margin-right: v-bind(selfModel.marginRight.active.xs.light);
		margin-bottom: v-bind(selfModel.marginBottom.active.xs.light);
		margin-left: v-bind(selfModel.marginLeft.active.xs.light);
	}

	.vp-navigator-item:focus {
		color: v-bind(selfModel.textColor.focus.xs.light);
		background-color: v-bind(selfModel.backgroundColor.focus.xs.light);
		background-image: v-bind(selfModel.backgroundImage.focus.xs.light);
		border-top-color: v-bind(selfModel.borderTopColor.focus.xs.light);
		border-right-color: v-bind(selfModel.borderRightColor.focus.xs.light);
		border-bottom-color: v-bind(selfModel.borderBottomColor.focus.xs.light);
		border-left-color: v-bind(selfModel.borderLeftColor.focus.xs.light);
		border-top-width: v-bind(selfModel.borderTopWidth.focus.xs.light);
		border-right-width: v-bind(selfModel.borderRightWidth.focus.xs.light);
		border-bottom-width: v-bind(selfModel.borderBottomWidth.focus.xs.light);
		border-left-width: v-bind(selfModel.borderLeftWidth.focus.xs.light);
		border-top-style: v-bind(selfModel.borderTopStyle.focus.xs.light);
		border-right-style: v-bind(selfModel.borderRightStyle.focus.xs.light);
		border-bottom-style: v-bind(selfModel.borderBottomStyle.focus.xs.light);
		border-left-style: v-bind(selfModel.borderLeftStyle.focus.xs.light);
		border-top-left-radius: v-bind(selfModel.borderTopLeftRadius.focus.xs.light);
		border-top-right-radius: v-bind(selfModel.borderTopRightRadius.focus.xs.light);
		border-bottom-right-radius: v-bind(selfModel.borderBottomRightRadius.focus.xs.light);
		border-bottom-left-radius: v-bind(selfModel.borderBottomLeftRadius.focus.xs.light);
		padding-top: v-bind(selfModel.paddingTop.focus.xs.light);
		padding-right: v-bind(selfModel.paddingRight.focus.xs.light);
		padding-bottom: v-bind(selfModel.paddingBottom.focus.xs.light);
		padding-left: v-bind(selfModel.paddingLeft.focus.xs.light);
		margin-top: v-bind(selfModel.marginTop.focus.xs.light);
		margin-right: v-bind(selfModel.marginRight.focus.xs.light);
		margin-bottom: v-bind(selfModel.marginBottom.focus.xs.light);
		margin-left: v-bind(selfModel.marginLeft.focus.xs.light);
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

	.vp-navigator-item--direction-right.vp-navigator-item--horizontal:not(.vp-navigator-item--level-0) > .vp-navigator-item--arrow,
	.vp-navigator-item--direction-right.vp-navigator-item--reverse.vp-navigator-item--horizontal.vp-navigator-item--level-1 .vp-navigator-item--arrow,
	.vp-navigator-item--direction-right.vp-navigator-item--drop-up.vp-navigator-item--reverse.vp-navigator-item--horizontal.vp-navigator-item--level-1 .vp-navigator-item--arrow {
		transform: rotate(0deg);
	}

	.vp-navigator-item--direction-left.vp-navigator-item--horizontal:not(.vp-navigator-item--level-0) > .vp-navigator-item--arrow,
	.vp-navigator-item--direction-left.vp-navigator-item--reverse.vp-navigator-item--horizontal.vp-navigator-item--level-1 .vp-navigator-item--arrow,
	.vp-navigator-item--direction-left.vp-navigator-item--drop-up.vp-navigator-item--reverse.vp-navigator-item--horizontal.vp-navigator-item--level-1 .vp-navigator-item--arrow {
		transform: rotate(-180deg);
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

	.vp-navigator-item--direction-right.vp-navigator-item--horizontal:not(.vp-navigator-item--level-0) > .wrapper {
		left: 100%;
		right: auto;
	}

	.vp-navigator-item--direction-left.vp-navigator-item--horizontal:not(.vp-navigator-item--level-0) > .wrapper {
		left: auto;
		right: 100%;
	}

	.vp-navigator-item--small,
	.vp-navigator-item--drop-up,
	.vp-navigator-item--odd,
	.vp-navigator-item--even,
	.vp-navigator-item--link {
		cursor: inherit;
	}

</style>