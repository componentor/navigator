<template>
	<div
		v-bind="$attrs"
		:class="{
			'vp-navigator--small': small,
			'vp-navigator--open': open || forceOpen,
			'vp-navigator--transition': transition,
			'vp-navigator--column': small || orientation === 'Column',
			'vp-navigator--reverse': ((orientation === 'Row' && !small) && direction === 'left') || ((orientation === 'Column' || small) && drop === 'up')
		}"
		:style="computedStyle"
		class="vp-navigator"
		@pointerover="hover=true"
		@pointerleave="hover=false"
	>
		<slot
			v-if="small"
			name="toggle"
			:isOpen="open || forceOpen"
			:toggle="toggleOpen"
			:style="toggleStyle"
			:icon="open || forceOpen ? $closeIcon : $toggleIcon"
		>
			<div
				@click.stop="toggleOpen"
				@pointerover="toggleHover=true"
				@pointerleave="toggleHover=false"
				:style="toggleStyle"
				class="vp-toggle"
			/>
		</slot>
		<template v-if="!small || open || forceOpen">
			<slot>
				<Placeholder />
			</slot>
		</template>
	</div>
	<Teleport
		v-if="isMounted && small && (open || forceOpen)"
		to="body"
	>
		<div
			ref="nav"
			:class="{
				'vp-navigator--small': small,
				'vp-navigator--open': open || forceOpen,
				'vp-navigator--transition': transition,
				'vp-navigator--column': small || orientation === 'Column',
				'vp-navigator--reverse': ((orientation === 'Row' && !small) && direction === 'left') || ((orientation === 'Column' || small) && drop === 'up')
			}"
			:style="computedModalStyle"
			class="vp-navigator"
			@pointerover="hover=true"
			@pointerleave="hover=false"
		>
			<slot
				v-if="small"
				name="toggle"
				:isOpen="open || forceOpen"
				:toggle="toggleOpen"
				:style="toggleStyleModal"
				:icon="open || forceOpen ? $closeIcon : $toggleIcon"
			>
				<div
					@click.stop="toggleOpen"
					@pointerover="toggleHover=true"
					@pointerleave="toggleHover=false"
					:style="toggleStyleModal"
					class="vp-toggle"
				/>
			</slot>
			<template v-if="!small || open || forceOpen">
				<slot>
					<Placeholder />
				</slot>
			</template>
		</div>
	</Teleport>
</template>
<script>
	import {
		computed
	} from 'vue';
	import {
		parse,
		getStyle
	} from '@componentor/breakpoint';
	import Placeholder from './Placeholder.vue';
	export default {
		inheritAttrs: false,
		inject: {
			theme: {
				default: ''
			},
			breakpoint: {
				default: ''
			}
		},
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
				center: computed(() => this.center),
				drop: computed(() => this.drop),
				level: computed(() => 0),
				order: computed(() => 'odd'),
				reverseIcon: computed(() => this.iconsReverse),
				childrenIconSizeProvider: computed(() => this.childrenIconSize),
				childrenCaretProvider: computed(() => this.parsedCaretIcon),
				childrenCaretSizeProvider: computed(() => this.caretSize),
				childrenCstyleProvider: computed(() => this.cstyleItem),
				childrenCstyleModalProvider: computed(() => this.cstyleItemModal),
				wrapperCstyleProvider: computed(() => this.cstyleDropArea),
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
			'$route'() {
				this.open = false;
			}
		},
		props: {
			toggleIcon: {
				type: String,
				default: ''
			},
			closeIcon: {
				type: String,
				default: ''
			},
			caretIcon: {
				type: String,
				default: ''
			},
			caretSize: {
				type: String,
				default: ''
			},
			toggleSize: {
				type: String,
				default: '40px'
			},
			iconsReverse: {
				type: Boolean,
				default: false
			},
			childrenIconSize: {
				type: String,
				default: ''
			},
			gap: {
				type: String,
				default: ''
			},
			childrenGap: {
				type: String,
				default: ''
			},
			orientation: {
				type: String,
				default: 'Row'
			},
			direction: {
				type: String,
				default: 'right'
			},
			center: {
				type: String,
				default: 'true'
			},
			drop: {
				type: String,
				default: 'down'
			},
			breakpointCap: {
				type: Number,
				default: 767
			},
			forceOpen: {
				type: Boolean,
				default: false
			},
			verticalLeftIndent: {
				type: String,
				default: ''
			},
			verticalRightIndent: {
				type: String,
				default: ''
			},
			cstyle: {
				type: [String, Object, Array],
				default: ''
			},
			cstyleModal: {
				type: [String, Object, Array],
				default: ''
			},
			cstyleToggle: {
				type: [String, Object, Array],
				default: ''
			},
			cstyleDropArea: {
				type: [String, Object, Array],
				default: ''
			},
			cstyleItem: {
				type: [String, Object, Array],
				default: ''
			},
			cstyleToggleModal: {
				type: [String, Object, Array],
				default: ''
			},
			cstyleItemModal: {
				type: [String, Object, Array],
				default: ''
			}
		},
		components: {
			Placeholder
		},
		data: () => ({
			open: false,
			hover: false,
			toggleHover: false,
			windowWidth: typeof global !== 'undefined' ? global?.windowWidth || 1280 : 1280,
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
				if (this.windowWidth <= Number(this.breakpointCap || 0)) return 'xs';
				if (this.breakpoint) return this.breakpoint;
				if (this.windowWidth < 640) return 'xs';
				if (this.windowWidth < 768) return 'sm';
				if (this.windowWidth < 1024) return 'md';
				if (this.windowWidth < 1280) return 'lg';
				if (this.windowWidth < 1536) return 'xl';
				return '2xl';
			},
			stateArray() {
				const states = [];
				if (this.hover) states.push('hover');
				return states;
			},
			toggleStateArray() {
				const states = [];
				if (this.toggleHover) states.push('hover');
				if (this.open || this.forceOpen) states.push('open');
				return states;
			},
			small() {
				return this.windowWidth <= Number(this.breakpointCap || 0);
			},
			cstyleString() {
				return this.normalizeCstyle(this.cstyle);
			},
			cstyleModalString() {
				return this.normalizeCstyle(this.cstyleModal) || this.cstyleString;
			},
			cstyleToggleString() {
				return this.normalizeCstyle(this.cstyleToggle);
			},
			cstyleToggleModalString() {
				return this.normalizeCstyle(this.cstyleToggleModal);
			},
			cstyleItemModalString() {
				return this.normalizeCstyle(this.cstyleItemModal);
			},
			computedStyle() {
				const baseStyle = {};
				if (this.cstyleString) {
					const parsed = parse(this.cstyleString);
					const style = getStyle(parsed, {
						theme: this.themeComputed,
						breakpoint: this.bpoint,
						states: this.stateArray,
						breakpointStrategy: 'mobile-first',
						themeStrategy: 'fallback'
					});
					Object.assign(baseStyle, this.parseStyleString(style));
				}
				if (!this.small && this.gap) {
					baseStyle.gap = this.gap;
				}
				return baseStyle;
			},
			computedModalStyle() {
				const baseStyle = {};
				if (this.cstyleModalString) {
					const parsed = parse(this.cstyleModalString);
					const style = getStyle(parsed, {
						theme: this.themeComputed,
						breakpoint: this.bpoint,
						states: this.stateArray,
						breakpointStrategy: 'mobile-first',
						themeStrategy: 'fallback'
					});
					Object.assign(baseStyle, this.parseStyleString(style));
				}
				if (!this.small && this.gap) {
					baseStyle.gap = this.gap;
				}
				return baseStyle;
			},
			toggleStyle() {
				const isOpen = this.open || this.forceOpen;
				const style = {
					backgroundImage: isOpen ? this.$closeIcon : this.$toggleIcon,
					width: this.toggleSize,
					zIndex: isOpen ? 10 : null
				};
				if (this.cstyleToggleString) {
					const parsed = parse(this.cstyleToggleString);
					const computedToggle = getStyle(parsed, {
						theme: this.themeComputed,
						breakpoint: this.bpoint,
						states: this.toggleStateArray,
						breakpointStrategy: 'mobile-first',
						themeStrategy: 'fallback'
					});
					Object.assign(style, this.parseStyleString(computedToggle));
				}
				return style;
			},
			toggleStyleModal() {
				const style = { ...this.toggleStyle };
				if (this.cstyleToggleModalString) {
					const parsed = parse(this.cstyleToggleModalString);
					const computedToggle = getStyle(parsed, {
						theme: this.themeComputed,
						breakpoint: this.bpoint,
						states: this.toggleStateArray,
						breakpointStrategy: 'mobile-first',
						themeStrategy: 'fallback'
					});
					Object.assign(style, this.parseStyleString(computedToggle));
				}
				return style;
			},
			$toggleIcon() {
				const icon = this.getThemedIcon(this.toggleIcon);
				if (!icon) return 'var(--menu-svg)';
				if (icon.startsWith('--')) {
					return `var(${icon})`;
				}
				return `url(${icon})`;
			},
			$closeIcon() {
				const icon = this.getThemedIcon(this.closeIcon);
				if (!icon) return 'var(--close-svg)';
				if (icon.startsWith('--')) {
					return `var(${icon})`;
				}
				return `url(${icon})`;
			},
			parsedCaretIcon() {
				return this.getThemedIcon(this.caretIcon);
			},
			model() {
				return {
					verticalLeftIndent: this.verticalLeftIndent,
					verticalRightIndent: this.verticalRightIndent,
					gap: this.childrenGap
				};
			}
		},
		mounted() {
			this.isMounted = true;
			this.windowWidth = window.innerWidth;
			document.cookie = `windowWidth=${window.innerWidth}; path=/; Secure; SameSite=None`;
			this.colorSchemeMediaQuery = window.matchMedia('(prefers-color-scheme: dark)');
			this.darkmode = window.matchMedia('(prefers-color-scheme: dark)').matches;
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
			normalizeCstyle(cstyle) {
				if (!cstyle) return '';
				if (typeof cstyle === 'string') return cstyle;
				if (Array.isArray(cstyle)) {
					return cstyle.map(item => {
						if (typeof item === 'string') return item;
						return Object.entries(item)
							.map(([key, value]) => `${key}:${value}`)
							.join('; ');
					}).join('; ');
				}
				return Object.entries(cstyle)
					.map(([key, value]) => `${key}:${value}`)
					.join('; ');
			},
			parseStyleString(styleStr) {
				if (!styleStr || typeof styleStr !== 'string') return {};
				const result = {};
				styleStr.split(';').forEach(part => {
					const [key, ...valueParts] = part.split(':');
					if (key && valueParts.length) {
						const trimmedKey = key.trim();
						const value = valueParts.join(':').trim();
						if (trimmedKey && value) {
							const camelKey = trimmedKey.replace(/-([a-z])/g, (_, c) => c.toUpperCase());
							result[camelKey] = value;
						}
					}
				});
				return result;
			},
			getThemedIcon(prop) {
				if (!prop) return '';
				// Try parsing as JSON structure with theme/breakpoint support
				try {
					const parsed = JSON.parse(prop.replaceAll('`', '"'));
					const themes = [this.themeComputed, 'light', 'dark'].filter(Boolean);
					const breakpoints = ['xs', 'sm', 'md', 'lg', 'xl', '2xl'];
					const groups = ['default', 'hover'];
					const limit = this.bpoint || 'xs';

					// Try to find a value matching current state
					for (const group of groups) {
						for (let i = 0; i < breakpoints.length; i++) {
							const breakpoint = breakpoints[i];
							for (const theme of themes) {
								const value = parsed?.[group]?.[breakpoint]?.[theme];
								if (value) return value;
							}
							if (breakpoint === limit) break;
						}
					}
					return '';
				} catch (e) {
					// Not JSON, return as-is (plain URL or CSS variable)
					return prop;
				}
			},
			toggleOpen() {
				this.open = !this.open;
			},
			handleColorSchemeChange(event) {
				this.darkmode = event.matches;
			},
			handleResize() {
				this.windowWidth = window.innerWidth;
				this.open = false;
			},
			handleClickOutside(event) {
				if (this.open && this.$refs.nav && !this.$refs.nav.contains(event.target)) {
					this.open = false;
				}
			}
		}
	};

</script>
<style scoped>
	* {
		--menu-svg: url(../assets/menu.svg);
		--close-svg: url(../assets/close.svg);
	}

	.vp-navigator {
		padding: 0px;
		overflow: visible;
		display: flex;
	}

	.vp-navigator--column {
		flex-direction: column;
	}

	.vp-navigator--reverse {
		flex-direction: row-reverse;
	}

	.vp-navigator--column.vp-navigator--reverse {
		flex-direction: column-reverse;
	}

	.vp-toggle {
		flex-shrink: 0;
		cursor: pointer;
		background-size: contain;
		background-repeat: no-repeat;
		background-position: center;
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
