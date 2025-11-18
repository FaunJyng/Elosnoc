{#snippet Icon()}
	{@const Icon = icon}
	<Icon {...options} />
{/snippet}

{@render Icon()}

<script module>
	export interface IconProps {
		icon: typeof LucideIcon;
		options?: LucideIconProps;
	}
</script>

<script lang="ts">
	import { type Icon as LucideIcon, type IconProps as LucideIconProps } from '@lucide/svelte';
	let { icon, options }: IconProps = $props();
</script>
