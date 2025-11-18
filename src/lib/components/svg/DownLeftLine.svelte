<style>
	svg {
		background-color: transparent;
	}
</style>

{#snippet leftLine()}
	<path
		d="
			M 0,8
			L {down.weight === 'bold' ? 8 + Weight.bold / 2 : 8},8
		"
		stroke={stroke.trim().length === 0 ? 'var(--primary-foreground)' : stroke}
		stroke-width={left.weight === 'light' ? Weight.light : Weight.bold}
		stroke-linecap="round"
	/>
{/snippet}

{#snippet downLine()}
	<path
		d="
			M 8,16
			L 8,8
		"
		stroke={stroke.trim().length === 0 ? 'var(--primary-foreground)' : stroke}
		stroke-width={down.weight === 'light' ? Weight.light : Weight.bold}
	/>
{/snippet}

<svg width={16} height={16} xmlns="http://www.w3.org/2000/svg">
	{@render leftLine()}
	{@render downLine()}
</svg>

<script module>
	import { Weight } from '$lib/components/svg/config/weight.js';

	type Variant = 'single' | 'double';

	export interface DownLeftLineProps {
		down?: {
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
		down = {
			variant: 'single',
			weight: 'light'
		},
		left = {
			variant: 'single',
			weight: 'light'
		},
		stroke = ''
	}: DownLeftLineProps = $props();
</script>
