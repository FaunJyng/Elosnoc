<style>
	svg {
		background-color: transparent;
	}
</style>

<svg width={16} {height} xmlns="http://www.w3.org/2000/svg" bind:clientHeight={svgClientHeight}>
	{#if variant === 'single'}
		<path
			id="single-line"
			d="
				M 8,0
				L 8,{svgClientHeight}
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

	export interface VLineProps {
		variant?: Variant;
		weight?: Weight;
		style?: Style;
		stroke?: string;
		height?: number | string;
	}
</script>

<script lang="ts">
	let {
		variant = 'single',
		weight = 'light',
		style = 'solid',
		stroke = '',
		height = '16'
	}: VLineProps = $props();
	let svgClientHeight: number = $state(0);
</script>
