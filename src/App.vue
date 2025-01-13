<template>
	<component
		:is="direction"
		class="vp-navigator"
		:class="{
			'vp-navigator--small': small
		}"
	>
		<Toggle
			v-if="small"
			icon="--menu-svg"
			:style="{
				width: iconSize
			}"
		/> <template v-else-if="!small">
			<slot>
				Drop Navigator Items Here
			</slot>
		</template>
	</component>
</template>
<script>
	import Column from '@vueplayio/column';
	import Row from '@vueplayio/row';
	import Toggle from '@/components/Toggle.vue';
	export default {
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
				default: 'horizontal',
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
			}
		}
	};

</script>
<style scoped>
	* {
		--menu-svg: url(@/assets/menu.svg);
	}

</style>