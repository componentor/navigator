<template>
	<component
		ref="nav"
		:is="small ? 'Column' : orientation"
		:class="{
			'vp-navigator--small': small
		}"
		class="vp-navigator"
	>
		<Toggle
			v-if="small && drop === 'down'"
			@click="open=!open"
			:open="open"
			:style="{
				width: toggleSize
			}"
			style="flex-shrink: 0"
			:icon="toggle"
		/> <template v-if="!small || open || forceOpen">
			<slot>
				<div style="padding:10px">
					Drop Navigator Items Here
				</div>
			</slot>
		</template>
		<Toggle
			v-if="small && drop === 'up'"
			@click="open=!open"
			:open="open"
			:style="{
				width: toggleSize
			}"
			style="flex-shrink: 0"
			:icon="toggle"
		/>
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
			};
		},
		props: {
			toggle: {
				type: String,
				control: 'media',
				default: '--menu-svg'
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
			}
		},
		created() {
			window.addEventListener('resize', this.handleResize);
		},
		mounted() {
			document.addEventListener('pointerdown', this.handleClickOutside)
		},
		beforeUnmount() {
			window.removeEventListener('resize', this.handleResize);
			document.removeEventListener('click', this.handleClickOutside)
		},
		methods: {
			handleResize() {
				this.screenWidth = window.innerWidth;
				this.open = false;
			},
			handleClickOutside(event) {
				if (this.open && this.$refs.nav && !this.$refs.nav.$el.contains(event.target)) {
					console.log('well')
					this.open = false
				}
			}
		}
	};

</script>
<style scoped>
	* {
		--menu-svg: url(@/assets/menu.svg);
	}

	.vp-navigator {
		padding: 0px;
		overflow: visible;
	}

</style>