<template>
	<Teleport
		to="body"
		:disabled="!open || !small"
	>
		<Box
			v-bind="$attrs"
			ref="nav"
			:column="(small || orientation === 'Column') ? '{`default`:{`xs`:{`light`:true}}}' : ''"
			:class="{
				'vp-navigator--small': small,
				'vp-navigator--open': open,
				'vp-navigator--transition': transition,
			}"
			:reverse="(((orientation === 'Row' && !small) && direction === 'left') || ((orientation === 'Column' || small) && drop === 'up')) ? '{`default`:{`xs`:{`light`:true}}}' : ''"
			:style="{
				backgroundColor: style?.backgroundColor,
				justifyContent: !open && small && style?.justifyToggle ? style?.justifyToggle : null,
				alignItems: !open && small && style?.alignToggle ? style?.alignToggle : null,
				gap: !small ? style?.gap : null
			}"
			class="vp-navigator"
			@pointerover="hover=true"
			@pointerleave="hover=false"
		>
			<div
				v-if="small"
				@click="open=!open"
				:style="{
					'background-image': open || forceOpen ? $closeIcon : $toggleIcon,
					'width': toggleSize
				}"
				class="vp-toggle"
			/> <template v-if="!small || open || forceOpen">
				<slot>
					<Placeholder />
				</slot>
			</template>
		</Box>
	</Teleport>
</template>
<script>
	import {
		computed
	} from 'vue';
	import Placeholder from '@/components/Placeholder.vue';
	import Box from '@vueplayio/box';
	export default {
		inject: ['theme', 'breakpoint'],
		provide() {
			return {
				open: computed(() => this.open),
				forceOpenProvider: computed(() => this.forceOpen),
				small: computed(() => this.small),
				orientation: computed(() => this.small ? 'Column' : this.orientation),
				direction: computed(() => this.direction),
				drop: computed(() => this.drop),
				reverseIcon: computed(() => this.iconsReverse),
				childrenIconSizeProvider: computed(() => this.childrenIconSize),
				childrenCaretProvider: computed(() => this.style.caretIcon),
				childrenCaretSizeProvider: computed(() => this.caretSize),
				model: computed(() => this.model),
				theme: computed(() => {
					if (this.theme) return this.theme;
					return this.darkmode ? 'dark' : 'light';
				}),
				breakpoint: computed(() => {
					if (this.breakpoint) return this.breakpoint;
					if (this.screenWidth > 1280) return '2xl';
					if (this.screenWidth > 1024) return 'xl';
					if (this.screenWidth > 768) return 'lg';
					if (this.screenWidth > 640) return 'md';
					if (this.screenWidth > 480) return 'sm';
					return 'xs';
				})
			};
		},
		watch: {
			open(open) {
				if (open && this.small) {
					setTimeout(() => {
						this.transition = !this.transition;
					});
				} else {
					this.transition = false;
				}
			}
		},
		props: {
			toggleIcon: {
				type: String,
				control: 'media',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			closeIcon: {
				type: String,
				control: 'media',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			caretIcon: {
				type: String,
				control: 'media',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			caretSize: {
				type: String,
				default: '',
				unit: 'px',
				control: 'slider'
			},
			toggleSize: {
				type: String,
				control: 'slider',
				unit: 'px',
				default: '40px'
			},
			justifyToggle: {
				type: String,
				default: '',
				options: [{
					value: '',
					key: 'Clear'
				}, {
					value: 'flex-start',
					key: 'flex-start'
				}, {
					value: 'flex-end',
					key: 'flex-end'
				}, {
					value: 'center',
					key: 'center'
				}, {
					value: 'space-between',
					key: 'space-between'
				}, {
					value: 'space-around',
					key: 'space-around'
				}, {
					value: 'space-evenly',
					key: 'space-evenly'
				}, {
					value: 'stretch',
					key: 'stretch'
				}, {
					value: 'normal',
					key: 'normal'
				}, {
					value: 'start',
					key: 'start'
				}, {
					value: 'end',
					key: 'end'
				}, {
					value: 'left',
					key: 'left'
				}, {
					value: 'right',
					key: 'right'
				}, {
					value: 'inherit',
					key: 'inherit'
				}, {
					value: 'initial',
					key: 'initial'
				}, {
					value: 'revert',
					key: 'revert'
				}, {
					value: 'revert-layer',
					key: 'revert-layer'
				}, {
					value: 'unset',
					key: 'unset'
				}],
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			alignToggle: {
				type: String,
				default: '',
				options: [{
					value: '',
					key: 'Clear'
				}, {
					value: 'anchor-center',
					key: 'anchor-center'
				}, {
					value: 'normal',
					key: 'normal'
				}, {
					value: 'stretch',
					key: 'stretch'
				}, {
					value: 'center',
					key: 'center'
				}, {
					value: 'start',
					key: 'start'
				}, {
					value: 'end',
					key: 'end'
				}, {
					value: 'self-start',
					key: 'self-start'
				}, {
					value: 'self-end',
					key: 'self-end'
				}, {
					value: 'flex-start',
					key: 'flex-start'
				}, {
					value: 'flex-end',
					key: 'flex-end'
				}, {
					value: 'baseline',
					key: 'baseline'
				}, {
					value: 'first baseline',
					key: 'first baseline'
				}, {
					value: 'last baseline',
					key: 'last baseline'
				}, {
					value: 'safe center',
					key: 'safe center'
				}, {
					value: 'unsafe center',
					key: 'unsafe center'
				}, {
					value: 'inherit',
					key: 'inherit'
				}, {
					value: 'initial',
					key: 'initial'
				}, {
					value: 'revert',
					key: 'revert'
				}, {
					value: 'revert-layer',
					key: 'revert-layer'
				}, {
					value: 'unset',
					key: 'unset'
				}],
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			iconsReverse: {
				type: Boolean,
				default: false
			},
			childrenIconSize: {
				type: String,
				default: '',
				unit: 'px',
				control: 'slider'
			},
			gap: {
				type: String,
				default: '',
				unit: 'px',
				control: 'slider',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			childrenGap: {
				type: String,
				default: '',
				unit: 'px',
				control: 'slider',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			orientation: {
				type: String,
				default: 'Row',
				options: [{
					key: 'Horizontal',
					value: 'Row'
				}, {
					key: 'Vertical',
					value: 'Column'
				}]
			},
			direction: {
				type: String,
				default: 'right',
				options: [{
					key: 'Right',
					value: 'right'
				}, {
					key: 'Left',
					value: 'left'
				}]
			},
			drop: {
				type: String,
				default: 'down',
				options: [{
					key: 'Downwards',
					value: 'down'
				}, {
					key: 'Upwards',
					value: 'up'
				}]
			},
			breakpointCap: {
				type: String,
				control: 'slider',
				unit: '',
				default: '480'
			},
			forceOpen: {
				type: Boolean,
				default: false
			},
			fontWeight: {
				type: String,
				default: '',
				control: 'slider',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			color: {
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
			backgroundColorDrop: {
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
				options: [{
					value: '',
					key: 'Clear'
				}, {
					value: 'none',
					key: 'none'
				}, {
					value: 'hidden',
					key: 'hidden'
				}, {
					value: 'solid',
					key: 'solid'
				}, {
					value: 'dashed',
					key: 'dashed'
				}, {
					value: 'dotted',
					key: 'dotted'
				}, {
					value: 'double',
					key: 'double'
				}, {
					value: 'groove',
					key: 'groove'
				}, {
					value: 'ridge',
					key: 'ridge'
				}, {
					value: 'inset',
					key: 'inset'
				}, {
					value: 'outset',
					key: 'outset'
				}],
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderRightStyle: {
				type: String,
				default: '',
				options: [{
					value: '',
					key: 'Clear'
				}, {
					value: 'none',
					key: 'none'
				}, {
					value: 'hidden',
					key: 'hidden'
				}, {
					value: 'solid',
					key: 'solid'
				}, {
					value: 'dashed',
					key: 'dashed'
				}, {
					value: 'dotted',
					key: 'dotted'
				}, {
					value: 'double',
					key: 'double'
				}, {
					value: 'groove',
					key: 'groove'
				}, {
					value: 'ridge',
					key: 'ridge'
				}, {
					value: 'inset',
					key: 'inset'
				}, {
					value: 'outset',
					key: 'outset'
				}],
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderBottomStyle: {
				type: String,
				default: '',
				options: [{
					value: '',
					key: 'Clear'
				}, {
					value: 'none',
					key: 'none'
				}, {
					value: 'hidden',
					key: 'hidden'
				}, {
					value: 'solid',
					key: 'solid'
				}, {
					value: 'dashed',
					key: 'dashed'
				}, {
					value: 'dotted',
					key: 'dotted'
				}, {
					value: 'double',
					key: 'double'
				}, {
					value: 'groove',
					key: 'groove'
				}, {
					value: 'ridge',
					key: 'ridge'
				}, {
					value: 'inset',
					key: 'inset'
				}, {
					value: 'outset',
					key: 'outset'
				}],
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderLeftStyle: {
				type: String,
				default: '',
				options: [{
					value: '',
					key: 'Clear'
				}, {
					value: 'none',
					key: 'none'
				}, {
					value: 'hidden',
					key: 'hidden'
				}, {
					value: 'solid',
					key: 'solid'
				}, {
					value: 'dashed',
					key: 'dashed'
				}, {
					value: 'dotted',
					key: 'dotted'
				}, {
					value: 'double',
					key: 'double'
				}, {
					value: 'groove',
					key: 'groove'
				}, {
					value: 'ridge',
					key: 'ridge'
				}, {
					value: 'inset',
					key: 'inset'
				}, {
					value: 'outset',
					key: 'outset'
				}],
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
			Placeholder,
			Box
		},
		data: () => ({
			open: false,
			hover: false,
			screenWidth: window.innerWidth,
			colorSchemeMediaQuery: null,
			darkmode: false,
			transition: false
		}),
		computed: {
			themeComputed() {
				if (this.theme) return this.theme;
				return this.darkmode ? 'dark' : 'light';
			},
			bpoint() {
				if (this.breakpoint) return this.breakpoint;
				if (this.screenWidth > 1280) return '2xl';
				if (this.screenWidth > 1024) return 'xl';
				if (this.screenWidth > 768) return 'lg';
				if (this.screenWidth > 640) return 'md';
				if (this.screenWidth > 480) return 'sm';
				return 'xs';
			},
			group() {
				if (this.hover) return 'hover';
				return 'default';
			},
			$toggleIcon() {
				if (!this.style?.toggleIcon) return 'var(--menu-svg)';
				if (this.style.toggleIcon?.startsWith('--')) {
					return `var(${this.style.toggleIcon})`;
				} else {
					return `url(${this.style.toggleIcon})`;
				}
			},
			$closeIcon() {
				if (!this.style?.closeIcon) return 'var(--close-svg)';
				if (this.style.closeIcon?.startsWith('--')) {
					return `var(${this.style.closeIcon})`;
				} else {
					return `url(${this.style.closeIcon})`;
				}
			},
			small() {
				return this.screenWidth <= this.breakpointCap;
			},
			model() {
				const obj = {};
				const props = ['fontWeight', 'gap', 'color', 'backgroundColor', 'backgroundColorDrop', 'backgroundImage', 'borderTopColor', 'borderRightColor', 'borderBottomColor', 'borderLeftColor', 'borderTopWidth', 'borderRightWidth', 'borderBottomWidth', 'borderLeftWidth', 'borderTopStyle', 'borderRightStyle', 'borderBottomStyle', 'borderLeftStyle', 'borderTopLeftRadius', 'borderTopRightRadius', 'borderBottomRightRadius', 'borderBottomLeftRadius', 'paddingTop', 'paddingRight', 'paddingBottom', 'paddingLeft', 'marginTop', 'marginRight', 'marginBottom', 'marginLeft'];
				for (const prop of props) {
					if (prop === 'gap' && this['childrenGap']) {
						try {
							obj[prop] = JSON.parse(this['childrenGap'].replaceAll('`', '"'));
						} catch (e) {}
					} else if (prop !== 'gap' && this[prop]) {
						try {
							obj[prop] = JSON.parse(this[prop].replaceAll('`', '"'));
						} catch (e) {}
					}
				}
				return obj;
			},
			style() {
				const style = {};
				const props = ['toggleIcon', 'closeIcon', 'caretIcon', 'justifyToggle', 'alignToggle', 'gap', 'backgroundColor'];
				const groups = ['default', 'hover'];
				const breakpoints = ['xs', 'sm', 'md', 'lg', 'xl', '2xl'];
				const themes = ['light', 'dark'];
				for (const prop of props) {
					let priority = {};
					if (this[prop]) {
						try {
							priority = JSON.parse(this[prop].replaceAll('`', '"'));
						} catch (e) {}
					}
					const merge = {};
					for (const group of Object.keys(priority)) {
						if (group === 'hover' && prop === 'backgroundColor') continue;
						const pri = priority?.[group] || {};
						merge[group] = {};
						for (const breakpoint of Object.keys(pri)) {
							const p = pri?.[breakpoint] || {};
							merge[group][breakpoint] = {};
							for (const theme of Object.keys(p)) {
								const value = p?.[theme]?.toString() || null;
								merge[group][breakpoint][theme] = value;
							}
						}
					}
					const groups = Object.keys(merge);
					if (groups.length) {
						style[prop] = merge?.['default']?.['xs']?.['light'];
						let limitReached = false;
						let limit = this.bpoint || 'xs';
						let match = false;
						for (const breakpoint of breakpoints) {
							if (!limitReached) {
								const firstPriority = merge?.[this.group]?.[breakpoint]?.[this.themeComputed]?.toString();
								const secondPriority = merge?.[this.group]?.[breakpoint]?.['light']?.toString();
								const value = firstPriority || secondPriority;
								if (value) {
									style[prop] = value;
									match = true;
								}
								limitReached = breakpoint === limit;
							}
						}
						if (!match && this.group !== 'default') {
							limitReached = false;
							limit = this.bpoint || 'xs';
							for (const breakpoint of breakpoints) {
								if (!limitReached) {
									const firstPriority = merge?.['default']?.[breakpoint]?.[this.themeComputed]?.toString();
									const secondPriority = merge?.['default']?.[breakpoint]?.['light']?.toString();
									const value = firstPriority || secondPriority;
									if (value) {
										style[prop] = value;
									}
									limitReached = breakpoint === limit;
								}
							}
						}
					}
				}
				return style;
			}
		},
		mounted() {
			this.colorSchemeMediaQuery = window.matchMedia('(prefers-color-scheme: dark)');
			this.darkmode = window.matchMedia('(prefers-color-scheme: dark)')
				.matches;
			this.colorSchemeMediaQuery.addEventListener('change', this.handleColorSchemeChange);
			document.addEventListener('click', this.handleClickOutside);
			window.addEventListener('resize', this.handleResize);
		},
		beforeUnmount() {
			this.colorSchemeMediaQuery.removeEventListener('change', this.handleColorSchemeChange);
			document.removeEventListener('click', this.handleClickOutside);
			window.removeEventListener('resize', this.handleResize);
		},
		methods: {
			renderProperty(prop) {
				return prop;
			},
			handleColorSchemeChange(event) {
				this.darkmode = event.matches;
			},
			handleResize() {
				this.screenWidth = window.innerWidth;
				this.open = false;
			},
			handleClickOutside(event) {
				if (this.open && this.$refs.nav && !this.$refs.nav.$el.contains(event.target)) {
					this.open = false;
				}
			}
		}
	};

</script>
<style scoped>
	* {
		--menu-svg: url(@/assets/menu.svg);
		--close-svg: url(@/assets/close.svg);
	}

	.vp-navigator {
		padding: 0px;
		overflow: visible;
	}

	.vp-toggle {
		flex-shrink: 0;
		cursor: pointer;
		background-size: contain;
		background-repeat: no-repeat;
		aspect-ratio: 1/1;
	}

	.vp-navigator--small.vp-navigator--open .vp-toggle {
		align-self: flex-end;
		margin: 10px;
	}

	.vp-navigator--small.vp-navigator--open {
		position: fixed;
		top: 0px;
		left: 0px;
		right: 0px;
		bottom: 0px;
		padding: 5px;
		height: 100vh !important;
		overflow-x: hidden !important;
		z-index: 100 !important;
	}

	.vp-navigator--small.vp-navigator--open.vp-navigator--transition {
		transition: border-color .3s linear, opacity .3s linear, color .3s linear, background .3s linear, background-color .3s linear;
	}

	.vp-navigator--small:not(.vp-navigator--open) {
		background-color: transparent !important;
	}

</style>