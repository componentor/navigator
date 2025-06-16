<template>
	<Box
		v-bind="$attrs"
		:column="(small || orientation === 'Column') ? '{`default`:{`xs`:{`light`:true}}}' : ''"
		:class="{
            'vp-navigator--small': small,
            'vp-navigator--open': open || forceOpen,
            'vp-navigator--transition': transition,
        }"
		:reverse="(((orientation === 'Row' && !small) && direction === 'left') || ((orientation === 'Column' || small) && drop === 'up')) ? '{`default`:{`xs`:{`light`:true}}}' : ''"
		:style="{
            backgroundColor: style?.backgroundColor,
            justifyContent: !open && !forceOpen && small && style?.justifyToggle ? style?.justifyToggle : null,
            alignItems: !open && !forceOpen && small && style?.alignToggle ? style?.alignToggle : null,
            gap: !small ? style?.gap : null
        }"
		class="vp-navigator"
		@pointerover="hover=true"
		@pointerleave="hover=false"
	>
		<div
			v-if="small"
			@click.stop="toggleOpen"
			:style="{
				'background-image': open || forceOpen ? $closeIcon : $toggleIcon,
				'width': toggleSize,
				'z-index': open || forceOpen ? 10 : null
			}"
			class="vp-toggle"
		/> <template v-if="!small || open || forceOpen">
			<slot>
				<Placeholder />
			</slot>
		</template>
	</Box>
	<Teleport v-if="isMounted && small && (open || forceOpen)" to="body">
		<Box
			ref="nav"
			:column="(small || orientation === 'Column') ? '{`default`:{`xs`:{`light`:true}}}' : ''"
			:class="{
				'vp-navigator--small': small,
				'vp-navigator--open': open || forceOpen,
				'vp-navigator--transition': transition,
			}"
			:reverse="(((orientation === 'Row' && !small) && direction === 'left') || ((orientation === 'Column' || small) && drop === 'up')) ? '{`default`:{`xs`:{`light`:true}}}' : ''"
			:style="{
				backgroundColor: style?.backgroundColorModal || style?.backgroundColor,
				justifyContent: !open && !forceOpen && small && style?.justifyToggle ? style?.justifyToggle : null,
				alignItems: !open && !forceOpen && small && style?.alignToggle ? style?.alignToggle : null,
				gap: !small ? style?.gap : null
			}"
			class="vp-navigator"
			@pointerover="hover=true"
			@pointerleave="hover=false"
		>
			<div
				v-if="small"
				@click.stop="toggleOpen"
				:style="{
					'transform': 'translate(' + (translateXToggle || 0) + ', ' + (translateYToggle || 0) + ')',
					'background-image': open || forceOpen ? $closeIcon : $toggleIcon,
					'width': toggleSize,
					'z-index': open || forceOpen ? 10 : null
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
			const self = this;
			return {
				setPath(path, id) {
					self.path = path;
					self.pathId = id;
				},
				path: computed(() => this.path),
				pathId: computed(() => this.pathId),
				open: computed(() => this.open),
				forceOpenProvider: computed(() => this.forceOpen),
				small: computed(() => this.small),
				orientation: computed(() => this.small ? 'Column' : this.orientation),
				direction: computed(() => this.direction),
				drop: computed(() => this.drop),
				reverseIcon: computed(() => this.iconsReverse),
				childrenIconSizeProvider: computed(() => this.childrenIconSize),
				childrenCaretProvider: computed(() => this.style?.caretIcon),
				childrenCaretSizeProvider: computed(() => this.caretSize),
				model: computed(() => this.model),
				theme: computed(() => {
					if (this.theme) return this.theme;
					return this.darkmode ? 'dark' : 'light';
				}),
				breakpoint: computed(() => {
					if (this.windowWidth <= Number(this.breakpointCap || 0)) return 'sm';
					if (this.breakpoint) return this.breakpoint;
					if (this.windowWidth > 1280) return '2xl';
					if (this.windowWidth > 1024) return 'xl';
					if (this.windowWidth > 768) return 'lg';
					if (this.windowWidth > 640) return 'md';
					if (this.windowWidth > 480) return 'sm';
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
			},
			'$router'() {
				this.open = false
			}
		},
		props: ['toggleIcon', 'closeIcon', 'caretIcon', 'caretSize', 'toggleSize', 'justifyToggle', 'alignToggle', 'iconsReverse', 'childrenIconSize', 'gap', 'childrenGap', 'orientation', 'direction', 'drop', 'breakpointCap', 'forceOpen', 'fontWeight', 'verticalLeftIndent', 'verticalRightIndent', 'color', 'backgroundColor', 'backgroundColorModal', 'backgroundColorDrop', 'backgroundImage', 'border', 'borderColor', 'borderTopColor', 'borderRightColor', 'borderBottomColor', 'borderLeftColor', 'borderWidth', 'borderTopWidth', 'borderRightWidth', 'borderBottomWidth', 'borderLeftWidth', 'borderStyle', 'borderTopStyle', 'borderRightStyle', 'borderBottomStyle', 'borderLeftStyle', 'borderRadius', 'borderTopLeftRadius', 'borderTopRightRadius', 'borderBottomRightRadius', 'borderBottomLeftRadius', 'translateXToggle', 'translateYToggle', 'paddingModal', 'paddingTopModal', 'paddingRightModal', 'paddingBottomModal', 'paddingLeftModal', 'padding', 'paddingTop', 'paddingRight', 'paddingBottom', 'paddingLeft', 'margin', 'marginTop', 'marginRight', 'marginBottom', 'marginLeft', 'position', 'justifyContent'],
		components: {
			Placeholder,
			Box
		},
		data: () => ({
			open: false,
			hover: false,
			windowWidth: typeof global !== 'undefined' ? (global?.windowWidth || 1280) : 1280,
			colorSchemeMediaQuery: null,
			darkmode: false,
			transition: false,
			path: '',
			pathId: '',
			isMounted: false
		}),
		computed: {
			themeComputed() {
				if (this.theme) return this.theme;
				return this.darkmode ? 'dark' : 'light';
			},
			bpoint() {
				if (this.windowWidth <= Number(this.breakpointCap || 0)) return 'sm';
				if (this.breakpoint) return this.breakpoint;
				if (this.windowWidth > 1280) return '2xl';
				if (this.windowWidth > 1024) return 'xl';
				if (this.windowWidth > 768) return 'lg';
				if (this.windowWidth > 640) return 'md';
				if (this.windowWidth > 480) return 'sm';
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
				return this.windowWidth <= Number(this.breakpointCap || 0);
			},
			model() {
				const obj = {};
				const props = ['fontWeight', 'gap', 'color', 'backgroundColor', 'backgroundColorDrop', 'verticalLeftIndent', 'verticalRightIndent', 'backgroundImage', 'border', 'borderColor', 'borderTopColor', 'borderRightColor', 'borderBottomColor', 'borderLeftColor', 'borderWidth', 'borderTopWidth', 'borderRightWidth', 'borderBottomWidth', 'borderLeftWidth', 'borderStyle', 'borderTopStyle', 'borderRightStyle', 'borderBottomStyle', 'borderLeftStyle', 'borderRadius', 'borderTopLeftRadius', 'borderTopRightRadius', 'borderBottomRightRadius', 'borderBottomLeftRadius', 'padding', 'paddingTop', 'paddingRight', 'paddingBottom', 'paddingLeft', 'margin', 'marginTop', 'marginRight', 'marginBottom', 'marginLeft', 'position', 'justifyContent'];
				for (const prop of props) {
					if (['verticalLeftIndent', 'verticalRightIndent'].includes(prop)) {
						obj[prop] = this[prop];
					} else if (prop === 'gap' && this['childrenGap']) {
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
				const scope = this
				const style = {};
				const props = ['toggleIcon', 'closeIcon', 'caretIcon', 'justifyToggle', 'alignToggle', 'gap', 'backgroundColor', 'backgroundColorModal'];
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
			this.isMounted = true
			this.windowWidth = window.innerWidth;
			document.cookie = `windowWidth=${window.innerWidth}; path=/; max-age=3600; Secure; SameSite=None`;
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
			toggleOpen() {
				this.open = !this.open
			},
			renderProperty(prop) {
				return prop;
			},
			handleColorSchemeChange(event) {
				this.darkmode = event.matches;
			},
			handleResize() {
				this.windowWidth = window.innerWidth;
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
		display: flex;
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
		padding: v-bind(paddingModal) !important;
		padding-top: v-bind(paddingTopModal) !important;
		padding-right: v-bind(paddingRightModal) !important;
		padding-bottom: v-bind(paddingBottomModal) !important;
		padding-left: v-bind(paddingLeftModal) !important;
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