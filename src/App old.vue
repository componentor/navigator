<template>
	<Teleport
		v-if="mounted"
		to="body"
		:disabled="(!open && !forceOpen) || !small"
	>
		<Navigator
			v-bind="$attrs"
			:title="title + ' mounted'"
			:toggleIcon="toggleIcon"
			:closeIcon="closeIcon"
			:caretIcon="caretIcon"
			:caretSize="caretSize"
			:toggleSize="toggleSize"
			:justifyToggle="justifyToggle"
			:alignToggle="alignToggle"
			:iconsReverse="iconsReverse"
			:childrenIconSize="childrenIconSize"
			:gap="gap"
			:childrenGap="childrenGap"
			:orientation="orientation"
			:direction="direction"
			:drop="drop"
			:breakpointCap="breakpointCap"
			:forceOpen="forceOpen"
			:fontWeight="fontWeight"
			:color="color"
			:backgroundColor="small && (open || forceOpen) ? backgroundColorModal : backgroundColor"
			:backgroundColorDrop="backgroundColorDrop"
			:backgroundImage="backgroundImage"
			:border="border"
			:borderColor="borderColor"
			:borderTopColor="borderTopColor"
			:borderRightColor="borderRightColor"
			:borderBottomColor="borderBottomColor"
			:borderLeftColor="borderLeftColor"
			:borderWidth="borderWidth"
			:borderTopWidth="borderTopWidth"
			:borderRightWidth="borderRightWidth"
			:borderBottomWidth="borderBottomWidth"
			:borderLeftWidth="borderLeftWidth"
			:borderStyle="borderStyle"
			:borderTopStyle="borderTopStyle"
			:borderRightStyle="borderRightStyle"
			:borderBottomStyle="borderBottomStyle"
			:borderLeftStyle="borderLeftStyle"
			:borderRadius="borderRadius"
			:borderTopLeftRadius="borderTopLeftRadius"
			:borderTopRightRadius="borderTopRightRadius"
			:borderBottomRightRadius="borderBottomRightRadius"
			:borderBottomLeftRadius="borderBottomLeftRadius"
			:translateXToggle="small && (open || forceOpen) ? translateXToggle : ''"
			:translateYToggle="small && (open || forceOpen) ? translateYToggle : ''"
			:paddingModal="paddingModal"
			:paddingTopModal="paddingTopModal"
			:paddingRightModal="paddingRightModal"
			:paddingBottomModal="paddingBottomModal"
			:paddingLeftModal="paddingLeftModal"
			:padding="padding"
			:paddingTop="paddingTop"
			:paddingRight="paddingRight"
			:paddingBottom="paddingBottom"
			:paddingLeft="paddingLeft"
			:margin="margin"
			:marginTop="marginTop"
			:marginRight="marginRight"
			:marginBottom="marginBottom"
			:marginLeft="marginLeft"
			:justifyContent="justifyContent"
			:position="position"
			:verticalLeftIndent="verticalLeftIndent"
			:verticalRightIndent="verticalRightIndent"
			@open="open = $event"
			@small="small = $event"
		>
			<slot>
				<Placeholder />
			</slot>
		</Navigator>
	</Teleport>
	<Navigator
		v-else-if="!mounted"
		v-bind="$attrs"
		:title="title + ' not mounted'"
		:toggleIcon="toggleIcon"
		:closeIcon="closeIcon"
		:caretIcon="caretIcon"
		:caretSize="caretSize"
		:toggleSize="toggleSize"
		:justifyToggle="justifyToggle"
		:alignToggle="alignToggle"
		:iconsReverse="iconsReverse"
		:childrenIconSize="childrenIconSize"
		:gap="gap"
		:childrenGap="childrenGap"
		:orientation="orientation"
		:direction="direction"
		:drop="drop"
		:breakpointCap="breakpointCap"
		:forceOpen="forceOpen"
		:fontWeight="fontWeight"
		:color="color"
		:backgroundColor="backgroundColor"
		:backgroundColorDrop="backgroundColorDrop"
		:backgroundImage="backgroundImage"
		:border="border"
		:borderColor="borderColor"
		:borderTopColor="borderTopColor"
		:borderRightColor="borderRightColor"
		:borderBottomColor="borderBottomColor"
		:borderLeftColor="borderLeftColor"
		:borderWidth="borderWidth"
		:borderTopWidth="borderTopWidth"
		:borderRightWidth="borderRightWidth"
		:borderBottomWidth="borderBottomWidth"
		:borderLeftWidth="borderLeftWidth"
		:borderStyle="borderStyle"
		:borderTopStyle="borderTopStyle"
		:borderRightStyle="borderRightStyle"
		:borderBottomStyle="borderBottomStyle"
		:borderLeftStyle="borderLeftStyle"
		:borderRadius="borderRadius"
		:borderTopLeftRadius="borderTopLeftRadius"
		:borderTopRightRadius="borderTopRightRadius"
		:borderBottomRightRadius="borderBottomRightRadius"
		:borderBottomLeftRadius="borderBottomLeftRadius"
		:paddingModal="paddingModal"
		:paddingTopModal="paddingTopModal"
		:paddingRightModal="paddingRightModal"
		:paddingBottomModal="paddingBottomModal"
		:paddingLeftModal="paddingLeftModal"
		:padding="padding"
		:paddingTop="paddingTop"
		:paddingRight="paddingRight"
		:paddingBottom="paddingBottom"
		:paddingLeft="paddingLeft"
		:margin="margin"
		:marginTop="marginTop"
		:marginRight="marginRight"
		:marginBottom="marginBottom"
		:marginLeft="marginLeft"
		:justifyContent="justifyContent"
		:position="position"
		:verticalLeftIndent="verticalLeftIndent"
		:verticalRightIndent="verticalRightIndent"
		@open="open = $event"
		@small="small = $event"
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
			title: {
				type: String
			},
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
			justifyToggle: {
				type: String,
				default: '',
				options: [{
					value: '',
					key: 'Clear'
				}, {
					value: 'flex-start',
					key: 'flex-start'
				}, {
					value: 'flex-end',
					key: 'flex-end'
				}, {
					value: 'center',
					key: 'center'
				}, {
					value: 'space-between',
					key: 'space-between'
				}, {
					value: 'space-around',
					key: 'space-around'
				}, {
					value: 'space-evenly',
					key: 'space-evenly'
				}, {
					value: 'stretch',
					key: 'stretch'
				}, {
					value: 'normal',
					key: 'normal'
				}, {
					value: 'start',
					key: 'start'
				}, {
					value: 'end',
					key: 'end'
				}, {
					value: 'left',
					key: 'left'
				}, {
					value: 'right',
					key: 'right'
				}, {
					value: 'inherit',
					key: 'inherit'
				}, {
					value: 'initial',
					key: 'initial'
				}, {
					value: 'revert',
					key: 'revert'
				}, {
					value: 'revert-layer',
					key: 'revert-layer'
				}, {
					value: 'unset',
					key: 'unset'
				}],
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			alignToggle: {
				type: String,
				default: '',
				options: [{
					value: '',
					key: 'Clear'
				}, {
					value: 'anchor-center',
					key: 'anchor-center'
				}, {
					value: 'normal',
					key: 'normal'
				}, {
					value: 'stretch',
					key: 'stretch'
				}, {
					value: 'center',
					key: 'center'
				}, {
					value: 'start',
					key: 'start'
				}, {
					value: 'end',
					key: 'end'
				}, {
					value: 'self-start',
					key: 'self-start'
				}, {
					value: 'self-end',
					key: 'self-end'
				}, {
					value: 'flex-start',
					key: 'flex-start'
				}, {
					value: 'flex-end',
					key: 'flex-end'
				}, {
					value: 'baseline',
					key: 'baseline'
				}, {
					value: 'first baseline',
					key: 'first baseline'
				}, {
					value: 'last baseline',
					key: 'last baseline'
				}, {
					value: 'safe center',
					key: 'safe center'
				}, {
					value: 'unsafe center',
					key: 'unsafe center'
				}, {
					value: 'inherit',
					key: 'inherit'
				}, {
					value: 'initial',
					key: 'initial'
				}, {
					value: 'revert',
					key: 'revert'
				}, {
					value: 'revert-layer',
					key: 'revert-layer'
				}, {
					value: 'unset',
					key: 'unset'
				}],
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
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
				default: 640
			},
			forceOpen: {
				type: Boolean,
				default: false
			},
			fontWeight: {
				type: Number,
				control: 'slider',
				min: 0,
				max: 1000,
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			color: {
				type: String,
				default: '',
				control: 'color',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			backgroundColor: {
				type: String,
				default: '',
				control: 'color',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			backgroundColorDrop: {
				type: String,
				default: '',
				control: 'color',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			backgroundColorModal: {
				type: String,
				default: '',
				control: 'color',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			backgroundImage: {
				type: String,
				default: '',
				control: 'media',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			border: {
				type: String,
				default: '',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderColor: {
				type: String,
				default: '',
				control: 'color',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderTopColor: {
				type: String,
				default: '',
				control: 'color',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderRightColor: {
				type: String,
				default: '',
				control: 'color',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderBottomColor: {
				type: String,
				default: '',
				control: 'color',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderLeftColor: {
				type: String,
				default: '',
				control: 'color',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderWidth: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderTopWidth: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderRightWidth: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderBottomWidth: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderLeftWidth: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderStyle: {
				type: String,
				default: '',
				options: [{
					value: '',
					key: 'Clear'
				}, {
					value: 'none',
					key: 'none'
				}, {
					value: 'hidden',
					key: 'hidden'
				}, {
					value: 'solid',
					key: 'solid'
				}, {
					value: 'dashed',
					key: 'dashed'
				}, {
					value: 'dotted',
					key: 'dotted'
				}, {
					value: 'double',
					key: 'double'
				}, {
					value: 'groove',
					key: 'groove'
				}, {
					value: 'ridge',
					key: 'ridge'
				}, {
					value: 'inset',
					key: 'inset'
				}, {
					value: 'outset',
					key: 'outset'
				}],
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderTopStyle: {
				type: String,
				default: '',
				options: [{
					value: '',
					key: 'Clear'
				}, {
					value: 'none',
					key: 'none'
				}, {
					value: 'hidden',
					key: 'hidden'
				}, {
					value: 'solid',
					key: 'solid'
				}, {
					value: 'dashed',
					key: 'dashed'
				}, {
					value: 'dotted',
					key: 'dotted'
				}, {
					value: 'double',
					key: 'double'
				}, {
					value: 'groove',
					key: 'groove'
				}, {
					value: 'ridge',
					key: 'ridge'
				}, {
					value: 'inset',
					key: 'inset'
				}, {
					value: 'outset',
					key: 'outset'
				}],
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderRightStyle: {
				type: String,
				default: '',
				options: [{
					value: '',
					key: 'Clear'
				}, {
					value: 'none',
					key: 'none'
				}, {
					value: 'hidden',
					key: 'hidden'
				}, {
					value: 'solid',
					key: 'solid'
				}, {
					value: 'dashed',
					key: 'dashed'
				}, {
					value: 'dotted',
					key: 'dotted'
				}, {
					value: 'double',
					key: 'double'
				}, {
					value: 'groove',
					key: 'groove'
				}, {
					value: 'ridge',
					key: 'ridge'
				}, {
					value: 'inset',
					key: 'inset'
				}, {
					value: 'outset',
					key: 'outset'
				}],
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderBottomStyle: {
				type: String,
				default: '',
				options: [{
					value: '',
					key: 'Clear'
				}, {
					value: 'none',
					key: 'none'
				}, {
					value: 'hidden',
					key: 'hidden'
				}, {
					value: 'solid',
					key: 'solid'
				}, {
					value: 'dashed',
					key: 'dashed'
				}, {
					value: 'dotted',
					key: 'dotted'
				}, {
					value: 'double',
					key: 'double'
				}, {
					value: 'groove',
					key: 'groove'
				}, {
					value: 'ridge',
					key: 'ridge'
				}, {
					value: 'inset',
					key: 'inset'
				}, {
					value: 'outset',
					key: 'outset'
				}],
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderLeftStyle: {
				type: String,
				default: '',
				options: [{
					value: '',
					key: 'Clear'
				}, {
					value: 'none',
					key: 'none'
				}, {
					value: 'hidden',
					key: 'hidden'
				}, {
					value: 'solid',
					key: 'solid'
				}, {
					value: 'dashed',
					key: 'dashed'
				}, {
					value: 'dotted',
					key: 'dotted'
				}, {
					value: 'double',
					key: 'double'
				}, {
					value: 'groove',
					key: 'groove'
				}, {
					value: 'ridge',
					key: 'ridge'
				}, {
					value: 'inset',
					key: 'inset'
				}, {
					value: 'outset',
					key: 'outset'
				}],
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderRadius: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderTopLeftRadius: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderTopRightRadius: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderBottomRightRadius: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			borderBottomLeftRadius: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			translateXToggle: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px'
			},
			translateYToggle: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px'
			},
			paddingModal: {
				type: String,
				default: '5px',
				control: 'slider',
				unit: 'px'
			},
			paddingTopModal: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px'
			},
			paddingRightModal: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px'
			},
			paddingBottomModal: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px'
			},
			paddingLeftModal: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px'
			},
			padding: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			paddingTop: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			paddingRight: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			paddingBottom: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			paddingLeft: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			margin: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			marginTop: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			marginRight: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			marginBottom: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			marginLeft: {
				type: String,
				default: '',
				control: 'slider',
				unit: 'px',
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			justifyContent: {
				type: String,
				default: '',
				options: [{
					value: '',
					key: 'Clear'
				}, {
					value: 'flex-start',
					key: 'flex-start'
				}, {
					value: 'flex-end',
					key: 'flex-end'
				}, {
					value: 'center',
					key: 'center'
				}, {
					value: 'space-between',
					key: 'space-between'
				}, {
					value: 'space-around',
					key: 'space-around'
				}, {
					value: 'space-evenly',
					key: 'space-evenly'
				}, {
					value: 'stretch',
					key: 'stretch'
				}, {
					value: 'normal',
					key: 'normal'
				}, {
					value: 'start',
					key: 'start'
				}, {
					value: 'end',
					key: 'end'
				}, {
					value: 'left',
					key: 'left'
				}, {
					value: 'right',
					key: 'right'
				}, {
					value: 'inherit',
					key: 'inherit'
				}, {
					value: 'initial',
					key: 'initial'
				}, {
					value: 'revert',
					key: 'revert'
				}, {
					value: 'revert-layer',
					key: 'revert-layer'
				}, {
					value: 'unset',
					key: 'unset'
				}],
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover', 'current', 'active', 'focus']
			},
			position: {
				type: String,
				default: '',
				options: [{
					value: '',
					key: 'Clear'
				}, {
					value: 'relative',
					key: 'relative'
				}, {
					value: 'absolute',
					key: 'absolute'
				}, {
					value: 'fixed',
					key: 'fixed'
				}, {
					value: 'sticky',
					key: 'sticky'
				}, {
					value: 'revert',
					key: 'revert'
				}, {
					value: 'static',
					key: 'static'
				}, {
					value: 'initial',
					key: 'initial'
				}, {
					value: 'inherit',
					key: 'inherit'
				}, {
					value: 'unset',
					key: 'unset'
				}],
				breakpoints: ['xs', 'sm', 'md', 'lg', 'xl', '2xl'],
				themes: ['light', 'dark'],
				groups: ['default', 'hover']
			}
		},
		data: () => ({
			open: false,
			small: false,
			mounted: false
		}),
		mounted() {
			console.log('nav loaded', this.title);
			this.mounted = true;
		}
	};

</script>
<style scoped></style>