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
		:orientation="orientation"
		:direction="direction"
		:center="centerDropdown"
		:drop="drop"
		:breakpointCap="breakpointCap"
		:breakpointStrategy="breakpointStrategy"
		:themeStrategy="themeStrategy"
		:forceOpen="forceOpen"
		:verticalLeftIndent="verticalLeftIndent"
		:verticalRightIndent="verticalRightIndent"
		:adapt="adapt"
		:adaptModal="adaptModal"
		:adaptToggle="adaptToggle"
		:adaptDropdown="adaptDropdown"
		:adaptIconWrapper="adaptIconWrapper"
		:adaptIcon="adaptIcon"
		:adaptLabel="adaptLabel"
		:adaptCaret="adaptCaret"
		:adaptCaretWrapper="adaptCaretWrapper"
		:adaptItem="adaptItem"
		:childrenAdaptItem="childrenAdaptItem"
		:childrenAdaptIconWrapper="childrenAdaptIconWrapper"
		:childrenAdaptIcon="childrenAdaptIcon"
		:childrenAdaptLabel="childrenAdaptLabel"
		:childrenAdaptCaret="childrenAdaptCaret"
		:childrenAdaptCaretWrapper="childrenAdaptCaretWrapper"
		:adaptToggleModal="adaptToggleModal"
		:adaptItemModal="adaptItemModal"
	>
		<slot>
			<Placeholder />
		</slot>
	</Navigator>
</template>
<script>
	import Navigator from './components/Navigator.vue';
	import Placeholder from './components/Placeholder.vue';
	export default {
		components: {
			Navigator,
			Placeholder
		},
		props: {
			toggleIcon: {
				type: String,
				control: 'media'
			},
			closeIcon: {
				type: String,
				control: 'media'
			},
			caretIcon: {
				type: String,
				control: 'media'
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
			adapt: {
				type: [String, Object, Array],
				default: ''
			},
			adaptModal: {
				type: [String, Object, Array],
				default: ''
			},
			adaptToggle: {
				type: [String, Object, Array],
				default: ''
			},
			adaptDropdown: {
				type: [String, Object, Array],
				default: ''
			},
			adaptIconWrapper: {
				type: [String, Object, Array],
				default: ''
			},
			adaptIcon: {
				type: [String, Object, Array],
				default: ''
			},
			adaptLabel: {
				type: [String, Object, Array],
				default: ''
			},
			adaptCaret: {
				type: [String, Object, Array],
				default: ''
			},
			adaptCaretWrapper: {
				type: [String, Object, Array],
				default: ''
			},
			adaptItem: {
				type: [String, Object, Array],
				default: ''
			},
			childrenAdaptItem: {
				type: [String, Object, Array],
				default: ''
			},
			childrenAdaptIconWrapper: {
				type: [String, Object, Array],
				default: ''
			},
			childrenAdaptIcon: {
				type: [String, Object, Array],
				default: ''
			},
			childrenAdaptLabel: {
				type: [String, Object, Array],
				default: ''
			},
			childrenAdaptCaret: {
				type: [String, Object, Array],
				default: ''
			},
			childrenAdaptCaretWrapper: {
				type: [String, Object, Array],
				default: ''
			},
			adaptToggleModal: {
				type: [String, Object, Array],
				default: ''
			},
			adaptItemModal: {
				type: [String, Object, Array],
				default: ''
			}
		}
	};

</script>
<style scoped></style>
