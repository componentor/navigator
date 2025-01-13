<template>
	<Row :class="{ 'vp-navigator-item--small': small }">
		{{ small ? 'small' : 'big'}}
		<template v-if="$slots.default">
			<div class="wrapper">
				<slot/>
			</div>
		</template>
		<router-link
			v-if="!external"
			:to="route"
			:target="target"
		>
			{{ title }}
		</router-link> <a
			v-else-if="external"
			:href="route"
			:target="target"
		>
			{{ title }}
		</a>
		<div
			:style="{
				'background-image': $icon
			}"
			style="background-size:contain;background-repeat:no-repeat;width:100%;aspect-ratio:1/1"
		/>
		
	</Row>
</template>
<script>
	import Row from '@vueplayio/row';
	export default {
		inject: ['small'],
		props: {
			title: {
				type: String,
				default: 'Title'
			},
			route: {
				type: String
			},
			icon: {
				type: String,
				control: 'media',
				default: '--vp-nav-default-icon'
			},
			external: {
				type: Boolean,
				default: false
			},
			target: {
				type: String,
				default: ''
			}
		},
		components: {
			Row: Row
		},
		data: () => ({}),
		mounted() {
			console.log('small', this.small)
		},
		computed: {
			$icon() {
				if (this.icon?.startsWith('--')) {
					return `var(${this.icon})`;
				} else {
					return `url(${this.icon})`;
				}
			}
		}
	};

</script>
<style scoped>
	* {
		--vp-nav-default-icon: url(@/assets/menu.svg);
	}
	.vp-navigator-item--small {
		background: blue
	}
</style>