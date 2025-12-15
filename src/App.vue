<template>
	<Navigator
		v-bind="$attrs"
		:toggleIcon="toggleIcon"
		:closeIcon="closeIcon"
		:caretIcon="caretIcon"
		:caretSize="caretSize"
		:toggleSize="toggleSize"
		:iconsReverse="iconsReverse"
		:childrenIconSize="childrenIconSize"
		:gap="gap"
		:childrenGap="childrenGap"
		:orientation="orientation"
		:direction="direction"
		:center="centerDropdown"
		:drop="drop"
		:breakpointCap="breakpointCap"
		:forceOpen="forceOpen"
		:verticalLeftIndent="verticalLeftIndent"
		:verticalRightIndent="verticalRightIndent"
		:cstyle="cstyle"
		:cstyleModal="cstyleModal"
		:cstyleToggle="cstyleToggle"
		:cstyleDropArea="cstyleDropArea"
		:cstyleItem="cstyleItem"
	>
		<slot>
			<Placeholder />
		</slot>
	</Navigator>
</template>
<script>
	import Navigator from '@/components/Navigator.vue';
	import Placeholder from '@/components/Placeholder.vue';
	export default {
		components: {
			Navigator,
			Placeholder
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
			verticalLeftIndent: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px'
			},
			verticalRightIndent: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px'
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
			centerDropdown: {
				type: String,
				default: 'true',
				options: [{
					key: 'Yes',
					value: 'true'
				}, {
					key: 'No',
					value: 'false'
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
				type: Number,
				control: 'slider',
				unit: '',
				default: 767
			},
			forceOpen: {
				type: Boolean,
				default: false
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
			}
		}
	};

</script>
<style scoped></style>
