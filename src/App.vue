<template>
	<component
		:is="direction"
		:class="{
			'vp-navigator--small': small
		}"
		class="vp-navigator"
	>
		<Toggle
			v-if="small"
			@click="open=!open"
			:open="open"
			:style="{
				width: iconSize
			}"
			style="flex-shrink: 0"
			icon="--menu-svg"
		/> <template v-if="!small || open">
			<slot>
				Drop Navigator Items Here
			</slot>
		</template>
	</component>
</template>
<script>
	import { computed } from 'vue'
	import Column from '@vueplayio/column';
	import Row from '@vueplayio/row';
	import Toggle from '@/components/Toggle.vue';
	export default {
		provide() {
			return {
				open: computed(() => this.open),
				small: computed(() => this.small),
				direction: computed(() => this.direction),
			}
		},
		props: {
			icon: {
				type: String,
				control: 'media',
				default: ''
			},
			iconSize: {
				type: String,
				control: 'slider',
				unit: 'px',
				default: '40px'
			},
			direction: {
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
			breakpoint: {
				type: String,
				control: 'slider',
				unit: '',
				default: '480'
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
		beforeUnmount() {
			window.removeEventListener('resize', this.handleResize);
		},
		methods: {
			handleResize() {
				this.screenWidth = window.innerWidth;
				this.open = false
			}
		}
	};

</script>
<style scoped>
	* {
		--menu-svg: url(@/assets/menu.svg);
	}
</style>