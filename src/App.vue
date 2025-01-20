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
		<Toggle
			v-if="small"
			@click="open=!open"
			:open="open || forceOpen"
			:style="{
				width: toggleSize
			}"
			style="flex-shrink: 0"
			:icon="toggleIcon"
			:iconClose="closeIcon"
		/> <template v-if="!small || open || forceOpen">
			<slot>
				<div style="padding:10px">
					Drop NavItems Here
				</div>
			</slot>
		</template>
	</component>
</template>
<script>
	import {
		computed
	} from 'vue';
	import Column from '@vueplayio/column';
	import Row from '@vueplayio/row';
	import Toggle from '@/components/Toggle.vue';
	const breakpoints = ['xs', 'sm', 'md', 'lg', 'xl', '2xl']
	const groups = ['default', 'hover', 'current', 'active', 'focus']
	const themes = ['light', 'dark']
	const borderStyleOptions = [
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
	]
	export default {
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
				model: computed(() => this.model)
			};
		},
		props: {
			toggleIcon: {
				type: String,
				control: 'media',
				default: '--menu-svg'
			},
			closeIcon: {
				type: String,
				control: 'media',
				default: '--close-svg'
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
			breakpoint: {
				type: String,
				control: 'slider',
				unit: '',
				default: '480'
			},
			forceOpen: {
				type: Boolean,
				default: false
			},
			textColor: {
				type: String,
				default: '',
				control: 'color',
				breakpoints,
				themes,
				groups
			},
			backgroundColor: {
				type: String,
				default: '',
				control: 'color',
				breakpoints,
				themes,
				groups
			},
			backgroundImage: {
				type: String,
				default: '',
				control: 'media',
				breakpoints,
				themes,
				groups
			},
			borderTopColor: {
				type: String,
				default: '',
				control: 'color',
				breakpoints,
				themes,
				groups
			},
			borderRightColor: {
				type: String,
				default: '',
				control: 'color',
				breakpoints,
				themes,
				groups
			},
			borderBottomColor: {
				type: String,
				default: '',
				control: 'color',
				breakpoints,
				themes,
				groups
			},
			borderLeftColor: {
				type: String,
				default: '',
				control: 'color',
				breakpoints,
				themes,
				groups
			},
			borderTopWidth: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints,
				themes,
				groups
			},
			borderRightWidth: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints,
				themes,
				groups
			},
			borderBottomWidth: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints,
				themes,
				groups
			},
			borderLeftWidth: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints,
				themes,
				groups
			},
			borderTopStyle: {
				type: String,
				default: '',
				options: borderStyleOptions,
				breakpoints,
				themes,
				groups
			},
			borderRightStyle: {
				type: String,
				default: '',
				options: borderStyleOptions,
				breakpoints,
				themes,
				groups
			},
			borderBottomStyle: {
				type: String,
				default: '',
				options: borderStyleOptions,
				breakpoints,
				themes,
				groups
			},
			borderLeftStyle: {
				type: String,
				default: '',
				options: borderStyleOptions,
				breakpoints,
				themes,
				groups
			},
			borderTopLeftRadius: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints,
				themes,
				groups
			},
			borderTopRightRadius: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints,
				themes,
				groups
			},
			borderBottomRightRadius: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints,
				themes,
				groups
			},
			borderBottomLeftRadius: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints,
				themes,
				groups
			},
			paddingTop: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints,
				themes,
				groups
			},
			paddingRight: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints,
				themes,
				groups
			},
			paddingBottom: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints,
				themes,
				groups
			},
			paddingLeft: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints,
				themes,
				groups
			},
			marginTop: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints,
				themes,
				groups
			},
			marginRight: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints,
				themes,
				groups
			},
			marginBottom: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints,
				themes,
				groups
			},
			marginLeft: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints,
				themes,
				groups
			}
		},
		components: {
			Column,
			Row,
			Toggle
		},
		data: () => ({
			open: false,
			screenWidth: window.innerWidth
		}),
		computed: {
			small() {
				return this.screenWidth <= this.breakpoint;
			},
			model() {
				const obj = {}
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
				]
				for (const prop of props) {
					obj[prop] = this[prop] ? JSON.parse(this[prop].replaceAll('`', '"')) : {
						default: {
							xs: { light: '', dark: '' },
							sm: { light: '', dark: '' },
							md: { light: '', dark: '' },
							lg: { light: '', dark: '' },
							xl: { light: '', dark: '' },
							'2xl': { light: '', dark: '' },
						}
					}
				}
				return obj
			}
		},
		created() {
			window.addEventListener('resize', this.handleResize);
		},
		mounted() {
			document.addEventListener('pointerdown', this.handleClickOutside);
		},
		beforeUnmount() {
			window.removeEventListener('resize', this.handleResize);
			document.removeEventListener('click', this.handleClickOutside);
		},
		methods: {
			renderProperty(prop) {
				return prop
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

</style>