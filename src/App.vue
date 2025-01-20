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
				breakpoints: ['2xl', 'xl', 'lg', 'md', 'sm'],
				themes: ['dark', 'light'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			backgroundColor: {
				type: String,
				default: '',
				control: 'color',
				breakpoints: ['2xl', 'xl', 'lg', 'md', 'sm'],
				themes: ['dark', 'light'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			backgroundImage: {
				type: String,
				default: '',
				control: 'media',
				breakpoints: ['2xl', 'xl', 'lg', 'md', 'sm'],
				themes: ['dark', 'light'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderColor: {
				type: String,
				default: '',
				control: 'color',
				breakpoints: ['2xl', 'xl', 'lg', 'md', 'sm'],
				themes: ['dark', 'light'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderTopColor: {
				type: String,
				default: '',
				control: 'color',
				breakpoints: ['2xl', 'xl', 'lg', 'md', 'sm'],
				themes: ['dark', 'light'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderRightColor: {
				type: String,
				default: '',
				control: 'color',
				breakpoints: ['2xl', 'xl', 'lg', 'md', 'sm'],
				themes: ['dark', 'light'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderBottomColor: {
				type: String,
				default: '',
				control: 'color',
				breakpoints: ['2xl', 'xl', 'lg', 'md', 'sm'],
				themes: ['dark', 'light'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderLeftColor: {
				type: String,
				default: '',
				control: 'color',
				breakpoints: ['2xl', 'xl', 'lg', 'md', 'sm'],
				themes: ['dark', 'light'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderWidth: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['2xl', 'xl', 'lg', 'md', 'sm'],
				themes: ['dark', 'light'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderTopWidth: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['2xl', 'xl', 'lg', 'md', 'sm'],
				themes: ['dark', 'light'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderRightWidth: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['2xl', 'xl', 'lg', 'md', 'sm'],
				themes: ['dark', 'light'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderBottomWidth: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['2xl', 'xl', 'lg', 'md', 'sm'],
				themes: ['dark', 'light'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderLeftWidth: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['2xl', 'xl', 'lg', 'md', 'sm'],
				themes: ['dark', 'light'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderStyle: {
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
				breakpoints: ['2xl', 'xl', 'lg', 'md', 'sm'],
				themes: ['dark', 'light'],
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
				breakpoints: ['2xl', 'xl', 'lg', 'md', 'sm'],
				themes: ['dark', 'light'],
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
				breakpoints: ['2xl', 'xl', 'lg', 'md', 'sm'],
				themes: ['dark', 'light'],
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
				breakpoints: ['2xl', 'xl', 'lg', 'md', 'sm'],
				themes: ['dark', 'light'],
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
				breakpoints: ['2xl', 'xl', 'lg', 'md', 'sm'],
				themes: ['dark', 'light'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderRadius: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['2xl', 'xl', 'lg', 'md', 'sm'],
				themes: ['dark', 'light'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderTopLeftRadius: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['2xl', 'xl', 'lg', 'md', 'sm'],
				themes: ['dark', 'light'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderTopRightRadius: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['2xl', 'xl', 'lg', 'md', 'sm'],
				themes: ['dark', 'light'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderBottomRightRadius: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['2xl', 'xl', 'lg', 'md', 'sm'],
				themes: ['dark', 'light'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderBottomLeftRadius: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['2xl', 'xl', 'lg', 'md', 'sm'],
				themes: ['dark', 'light'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			padding: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['2xl', 'xl', 'lg', 'md', 'sm'],
				themes: ['dark', 'light'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			paddingTop: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['2xl', 'xl', 'lg', 'md', 'sm'],
				themes: ['dark', 'light'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			paddingRight: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['2xl', 'xl', 'lg', 'md', 'sm'],
				themes: ['dark', 'light'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			paddingBottom: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['2xl', 'xl', 'lg', 'md', 'sm'],
				themes: ['dark', 'light'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			paddingLeft: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['2xl', 'xl', 'lg', 'md', 'sm'],
				themes: ['dark', 'light'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			margin: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['2xl', 'xl', 'lg', 'md', 'sm'],
				themes: ['dark', 'light'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			marginTop: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['2xl', 'xl', 'lg', 'md', 'sm'],
				themes: ['dark', 'light'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			marginRight: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['2xl', 'xl', 'lg', 'md', 'sm'],
				themes: ['dark', 'light'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			marginBottom: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['2xl', 'xl', 'lg', 'md', 'sm'],
				themes: ['dark', 'light'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			marginLeft: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['2xl', 'xl', 'lg', 'md', 'sm'],
				themes: ['dark', 'light'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
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
					'borderColor',
					'borderTopColor',
					'borderRightColor',
					'borderBottomColor',
					'borderLeftColor',
					'borderWidth',
					'borderTopWidth',
					'borderRightWidth',
					'borderBottomWidth',
					'borderLeftWidth',
					'borderStyle',
					'borderTopStyle',
					'borderRightStyle',
					'borderBottomStyle',
					'borderLeftStyle',
					'borderRadius',
					'borderTopLeftRadius',
					'borderTopRightRadius',
					'borderBottomRightRadius',
					'borderBottomLeftRadius',
					'padding',
					'paddingTop',
					'paddingRight',
					'paddingBottom',
					'paddingLeft',
					'margin',
					'marginTop',
					'marginRight',
					'marginBottom',
					'marginLeft',
				]
				for (const prop of props) {
					obj[prop] = this[prop] ? JSON.parse(this[prop]) : {
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