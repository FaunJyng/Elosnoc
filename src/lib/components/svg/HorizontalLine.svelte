<style>
	svg {
		background-color: transparent;
	}
</style>

<svg {width} height={16} xmlns="http://www.w3.org/2000/svg" bind:clientWidth={svgClientWidth}>
	{#if variant === 'single'}
		<path
			id="single-line"
			d="
				M 0,8
				L {svgClientWidth},8
			"
			stroke={stroke.trim().length === 0 ? 'var(--primary-foreground)' : stroke}
			stroke-width={weight === 'light' ? Weight.light : Weight.bold}
			stroke-linecap="square"
		/>
	{/if}
</svg>

<script module>
	import { Weight } from '$lib/components/svg/config/weight.js';

	type Variant = 'single' | 'double';
	type Style = 'solid' | 'dashed';

	export interface HLineProps {
		variant?: Variant;
		weight?: Weight;
		style?: Style;
		stroke?: string;
		width?: number | string;
	}
</script>

<script lang="ts">
	let {
		variant = 'single',
		weight = 'light',
		style = 'solid',
		stroke = '',
		width = '16'
	}: HLineProps = $props();
	let svgClientWidth: number = $state(0);
</script>
