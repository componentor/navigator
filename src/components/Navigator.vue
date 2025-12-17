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
				childrenCaretProvider: computed(() => this.caretIcon),
				childrenCaretSizeProvider: computed(() => this.caretSize),
				childrenCstyleProvider: computed(() => this.childrenCstyleItem),
				childrenCstyleModalProvider: computed(() => this.cstyleItemModal),
				cstyleProvider: computed(() => this.cstyleItem),
				wrapperCstyleProvider: computed(() => this.cstyleDropArea),
				iconWrapperCstyleProvider: computed(() => this.cstyleIconWrapper),
				iconCstyleProvider: computed(() => this.cstyleIcon),
				linkCstyleProvider: computed(() => this.cstyleLink),
				caretWrapperCstyleProvider: computed(() => this.cstyleCaretWrapper),
				caretCstyleProvider: computed(() => this.cstyleCaret),
				childrenCstyleIconWrapperProvider: computed(() => this.childrenCstyleIconWrapper),
				childrenCstyleIconProvider: computed(() => this.childrenCstyleIcon),
				childrenCstyleLinkProvider: computed(() => this.childrenCstyleLink),
				childrenCstyleCaretWrapperProvider: computed(() => this.childrenCstyleCaretWrapper),
				childrenCstyleCaretProvider: computed(() => this.childrenCstyleCaret),
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
			breakpointStrategy: {
				type: String,
				default: 'mobile-first',
				validator: v => ['exact', 'mobile-first', 'desktop-first'].includes(v)
			},
			themeStrategy: {
				type: String,
				default: 'fallback',
				validator: v => ['strict', 'fallback'].includes(v)
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
				default: 'display:flex; gap:4px; background-color:#ffffff; dark:background-color:#1a1a1a; padding:8px'
			},
			cstyleModal: {
				type: [String, Object, Array],
				default: 'background-color:rgba(255,255,255,0.98); dark:background-color:rgba(0,0,0,0.95); padding:20px'
			},
			cstyleToggle: {
				type: [String, Object, Array],
				default: ''
			},
			cstyleDropArea: {
				type: [String, Object, Array],
				default: 'background-color:#ffffff; dark:background-color:#2a2a2a; box-shadow:0 2px 8px rgba(0,0,0,0.1); dark:box-shadow:0 2px 8px rgba(0,0,0,0.3); border-radius:4px; padding:4px'
			},
			cstyleIconWrapper: {
				type: [String, Object, Array],
				default: ''
			},
			cstyleIcon: {
				type: [String, Object, Array],
				default: ''
			},
			cstyleLink: {
				type: [String, Object, Array],
				default: ''
			},
			cstyleCaret: {
				type: [String, Object, Array],
				default: ''
			},
			cstyleCaretWrapper: {
				type: [String, Object, Array],
				default: ''
			},
			cstyleItem: {
				type: [String, Object, Array],
				default: 'padding:12px 16px; border-radius:4px; hover:background-color:rgba(0,0,0,0.05); dark:hover:background-color:rgba(255,255,255,0.1); current:font-weight:600; current:color:#0066cc; dark:current:color:#66b3ff'
			},
			childrenCstyleItem: {
				type: [String, Object, Array],
				default: 'padding:10px 16px; border-radius:4px; hover:background-color:rgba(0,0,0,0.05); dark:hover:background-color:rgba(255,255,255,0.1); current:font-weight:600; current:color:#0066cc; dark:current:color:#66b3ff'
			},
			childrenCstyleIconWrapper: {
				type: [String, Object, Array],
				default: ''
			},
			childrenCstyleIcon: {
				type: [String, Object, Array],
				default: ''
			},
			childrenCstyleLink: {
				type: [String, Object, Array],
				default: ''
			},
			childrenCstyleCaret: {
				type: [String, Object, Array],
				default: ''
			},
			childrenCstyleCaretWrapper: {
				type: [String, Object, Array],
				default: ''
			},
			cstyleToggleModal: {
				type: [String, Object, Array],
				default: ''
			},
			cstyleItemModal: {
				type: [String, Object, Array],
				default: 'padding:14px 20px; border-radius:4px; hover:background-color:rgba(0,0,0,0.05); dark:hover:background-color:rgba(255,255,255,0.1); current:font-weight:600; current:color:#0066cc; dark:current:color:#66b3ff; font-size:16px'
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
			isMounted: false,
			resizeTimeout: null
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
				return this.computeCstyleToStyleObject(this.cstyleString);
			},
			computedModalStyle() {
				return this.computeCstyleToStyleObject(this.cstyleModalString);
			},
			toggleStyle() {
				const isOpen = this.open || this.forceOpen;
				const baseStyle = {
					backgroundImage: isOpen ? this.$closeIcon : this.$toggleIcon,
					width: this.toggleSize,
					zIndex: isOpen ? 10 : null
				};
				const cstyleObject = this.computeToggleCstyleToStyleObject(this.cstyleToggleString);
				return { ...baseStyle, ...cstyleObject };
			},
			toggleStyleModal() {
				const baseStyle = { ...this.toggleStyle };
				const cstyleObject = this.computeToggleCstyleToStyleObject(this.cstyleToggleModalString);
				return { ...baseStyle, ...cstyleObject };
			},
			$toggleIcon() {
				const icon = this.toggleIcon;
				if (!icon) return this.theme === 'dark' ? 'var(--menu-svg-light)' : 'var(--menu-svg)';
				if (icon.startsWith('--')) {
					return `var(${icon})`;
				}
				return `url(${icon})`;
			},
			$closeIcon() {
				const icon = this.closeIcon;
				if (!icon) return this.theme === 'dark' ? 'var(--close-svg-light)' : 'var(--close-svg)';
				if (icon.startsWith('--')) {
					return `var(${icon})`;
				}
				return `url(${icon})`;
			},
			model() {
				return {
					verticalLeftIndent: this.verticalLeftIndent,
					verticalRightIndent: this.verticalRightIndent
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
			if (this.resizeTimeout) clearTimeout(this.resizeTimeout);
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
			computeCstyleToStyleObject(cstyleString) {
				if (!cstyleString) return {};
				const parsed = parse(cstyleString);
				const style = getStyle(parsed, {
					theme: this.themeComputed,
					breakpoint: this.bpoint,
					states: this.stateArray,
					breakpointStrategy: this.breakpointStrategy,
					themeStrategy: this.themeStrategy
				});
				return this.parseStyleString(style);
			},
			computeToggleCstyleToStyleObject(cstyleString) {
				if (!cstyleString) return {};
				const parsed = parse(cstyleString);
				const style = getStyle(parsed, {
					theme: this.themeComputed,
					breakpoint: this.bpoint,
					states: this.toggleStateArray,
					breakpointStrategy: this.breakpointStrategy,
					themeStrategy: this.themeStrategy
				});
				return this.parseStyleString(style);
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
			toggleOpen() {
				this.open = !this.open;
			},
			handleColorSchemeChange(event) {
				this.darkmode = event.matches;
			},
			handleResize() {
				if (this.resizeTimeout) clearTimeout(this.resizeTimeout);
				this.resizeTimeout = setTimeout(() => {
					this.windowWidth = window.innerWidth;
					this.open = false;
				}, 150);
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
		--menu-svg-light: url(../assets/light/menu.svg);
		--close-svg-light: url(../assets/light/close.svg);
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
