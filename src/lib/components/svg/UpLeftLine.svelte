<style>
	svg {
		background-color: transparent;
	}
</style>

{#snippet leftLine()}
	<path
		d="
			M 0,8
			L {up.weight === 'bold' ? 8 + Weight.bold / 2 : 8},8
		"
		stroke={stroke.trim().length === 0 ? 'var(--primary-foreground)' : stroke}
		stroke-width={left.weight === 'light' ? Weight.light : Weight.bold}
	/>
{/snippet}

{#snippet upLine()}
	<path
		d="
			M 8,0
			L 8,{left.weight === 'bold' ? 8 + Weight.bold / 2 : 8}
		"
		stroke={stroke.trim().length === 0 ? 'var(--primary-foreground)' : stroke}
		stroke-width={up.weight === 'light' ? Weight.light : Weight.bold}
	/>
{/snippet}

<svg width={16} height={16} xmlns="http://www.w3.org/2000/svg">
	{@render leftLine()}
	{@render upLine()}
</svg>

<script module>
	import { Weight } from '$lib/components/svg/config/weight.js';

	type Variant = 'single' | 'double';

	export interface DownRightLineProps {
		up?: {
			variant?: Variant;
			weight?: Weight;
		};
		left?: {
			variant?: Variant;
			weight?: Weight;
		};
		stroke?: string;
	}
</script>

<script lang="ts">
	let {
		up = {
			variant: 'single',
			weight: 'light'
		},
		left = {
			variant: 'single',
			weight: 'light'
		},
		stroke = ''
	}: DownRightLineProps = $props();
</script>
