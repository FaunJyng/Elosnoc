<style>
	svg {
		background-color: transparent;
	}
</style>

{#snippet rightLine()}
	<path
		d="
			M 16,8
			L {down.weight === 'bold' ? 8 - Weight.bold / 2 : 8},8
		"
		stroke={stroke.trim().length === 0 ? 'var(--primary-foreground)' : stroke}
		stroke-width={right.weight === 'light' ? Weight.light : Weight.bold}
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
	{@render rightLine()}
	{@render downLine()}
</svg>

<script module>
	import { Weight } from '$lib/components/svg/config/weight.js';

	type Variant = 'single' | 'double';

	export interface DownRightLineProps {
		down?: {
			variant?: Variant;
			weight?: Weight;
		};
		right?: {
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
		right = {
			variant: 'single',
			weight: 'light'
		},
		stroke = ''
	}: DownRightLineProps = $props();
</script>
