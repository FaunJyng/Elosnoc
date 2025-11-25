<style>
	.container {
		display: flex;
		flex-direction: row;
	}
</style>

<span style:display="none">
	{@render children?.()}
</span>

<div class="container" style:flex-direction={direction}>
	{#if direction === 'row'}
		{#each buttonsProps as buttonProps, i (i)}
			{#if i !== 0}
				<Button {...buttonProps} mode="normal" --btn-lb-width="0px" />
			{:else}
				<Button {...buttonProps} mode="normal" />
			{/if}
		{/each}
	{:else}
		{#each buttonsProps as buttonProps, i (i)}
			{#if i !== buttonsProps.length - 1}
				<Button {...buttonProps} mode="normal" --btn-bb-width="0px" />
			{:else}
				<Button {...buttonProps} mode="normal" />
			{/if}
		{/each}
	{/if}
</div>

<script module>
	import { createContext, type Snippet } from 'svelte';
	import Button, { type ButtonProps } from './Button.svelte';

	const [getButtonGroupContext, setButtonGroupContext] = createContext<ButtonProps[]>();

	export { getButtonGroupContext };

	export type ButtonGroupCustomProp = {
		children?: Snippet;
		layout?: 'column' | 'row';
	};
</script>

<script lang="ts">
	let { children, layout: direction = 'row' }: ButtonGroupCustomProp = $props();
	let buttonsProps: ButtonProps[] = $state([]);

	setButtonGroupContext(buttonsProps);
</script>
