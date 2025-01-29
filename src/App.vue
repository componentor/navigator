<template>
	<component
		ref="nav"
		:is="small ? 'Column' : orientation"
		:class="{
			'vp-navigator--small': small
		}"
		:reverse="((orientation === 'Row' && !small) && direction === 'left') || ((orientation === 'Column' || small) && drop === 'up')"
		class="vp-navigator"
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
	</component>
</template>
<script>
	import {
		computed
	} from 'vue';
	import Placeholder from '@/components/Placeholder.vue';
	import Column from '@vueplayio/column';
	import Row from '@vueplayio/row';
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
				childrenCaretProvider: computed(() => this.childrenCaret),
				childrenCaretSizeProvider: computed(() => this.childrenCaretSize),
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
		props: {
			toggleIcon: {
				type: String,
				control: 'media',
				default: '--menu-svg',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			closeIcon: {
				type: String,
				control: 'media',
				default: '--close-svg',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			toggleSize: {
				type: String,
				control: 'slider',
				unit: 'px',
				default: '40px'
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
			Column,
			Row
		},
		data: () => ({
			open: false,
			screenWidth: window.innerWidth,
			colorSchemeMediaQuery: null,
			darkmode: false
		}),
		computed: {
			$toggleIcon() {
				if (this.toggleIcon?.startsWith('--')) {
					return `var(${this.toggleIcon})`;
				} else {
					return `url(${this.toggleIcon})`;
				}
			},
			$closeIcon() {
				if (this.closeIcon?.startsWith('--')) {
					return `var(${this.closeIcon})`;
				} else {
					return `url(${this.closeIcon})`;
				}
			},
			small() {
				return this.screenWidth <= this.breakpointCap;
			},
			model() {
				const obj = {};
				const props = ['fontWeight', 'color', 'backgroundColor', 'backgroundImage', 'borderTopColor', 'borderRightColor', 'borderBottomColor', 'borderLeftColor', 'borderTopWidth', 'borderRightWidth', 'borderBottomWidth', 'borderLeftWidth', 'borderTopStyle', 'borderRightStyle', 'borderBottomStyle', 'borderLeftStyle', 'borderTopLeftRadius', 'borderTopRightRadius', 'borderBottomRightRadius', 'borderBottomLeftRadius', 'paddingTop', 'paddingRight', 'paddingBottom', 'paddingLeft', 'marginTop', 'marginRight', 'marginBottom', 'marginLeft'];
				for (const prop of props) {
					if (this[prop]) {
						obj[prop] = JSON.parse(this[prop].replaceAll('`', '"'));
					}
				}
				return obj;
			}
		},
		mounted() {
			this.colorSchemeMediaQuery = window.matchMedia('(prefers-color-scheme: dark)');
			this.darkmode = window.matchMedia('(prefers-color-scheme: dark)')
				.matches;
			this.colorSchemeMediaQuery.addEventListener('change', this.handleColorSchemeChange);
			document.addEventListener('pointerdown', this.handleClickOutside);
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

</style>