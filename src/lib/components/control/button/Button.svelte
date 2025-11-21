<style>
	button {
		display: flex;
		align-items: center;
		justify-content: center;
		border-top: 1px solid var(--primary-foreground);
		border-right: 1px solid var(--primary-foreground);
		border-left: 3px solid var(--primary-foreground);
		border-bottom: 3px solid var(--primary-foreground);
	}

	.label,
	.icon {
		background-color: transparent;
	}

	.label {
		padding: calc(var(--line-height) / 2) var(--line-height);
	}

	.icon {
		display: flex;
		height: -webkit-fill-available;
		align-items: center;
		justify-content: center;
		padding-left: calc(var(--line-height) / 1.5);
		padding-right: calc(var(--line-height) / 1.5);
	}

	.icon-front {
		border-right: 1px solid var(--primary-foreground);
	}

	.icon-back {
		border-left: 1px solid var(--primary-foreground);
	}
</style>

<button
	onmousedown={() => (mouseState = ButtonMouseState.Mousedown)}
	onmouseup={() => (mouseState = ButtonMouseState.Mouseup)}
	onmouseleave={() => (mouseState = ButtonMouseState.Mouseleave)}
	onmouseenter={() => (mouseState = ButtonMouseState.Mouseenter)}
	bind:this={ref}
	{...rest}
	style:background-color={mouseState === ButtonMouseState.Mousedown
		? 'var(--primary-hover)'
		: 'var(--primary)'}
	style:color={mouseState === ButtonMouseState.Mousedown
		? 'var(--primary-foreground-hover)'
		: 'var(--primary-foreground)'}
	style:border-left-width={mouseState === ButtonMouseState.Mouseenter ||
	mouseState === ButtonMouseState.Mouseup
		? '1px'
		: '3px'}
	style:border-bottom-width={mouseState === ButtonMouseState.Mouseenter ||
	mouseState === ButtonMouseState.Mouseup
		? '1px'
		: '3px'}
>
	{#if icon}
		{#if iconPosition === 'back'}
			<div class="label">
				{@render children?.()}
			</div>
			<div
				class="icon icon-back"
				style:border-left-color={mouseState === ButtonMouseState.Mousedown
					? 'var(--primary-foreground-hover)'
					: 'var(--primary-foreground)'}
			>
				{@render icon?.()}
			</div>
		{:else}
			<div
				class="icon icon-front"
				style:border-right-color={mouseState === ButtonMouseState.Mousedown
					? 'var(--primary-foreground-hover)'
					: 'var(--primary-foreground)'}
			>
				{@render icon?.()}
			</div>
			<div class="label">
				{@render children?.()}
			</div>
		{/if}
	{:else}
		<div class="label">
			{@render children?.()}
		</div>
	{/if}
</button>

<script module>
	import type { HTMLButtonAttributes } from 'svelte/elements';
	import { type Snippet } from 'svelte';

	export interface ButtonProps {
		ref?: HTMLButtonElement | null;
		icon?: Snippet;
		mouseState?: ButtonMouseState;
		iconPosition?: 'front' | 'back';
	}

	export const ButtonMouseState = {
		Mouseenter: 'Mouseenter',
		Mouseleave: 'Mouseleave',
		Mousedown: 'Mousedown',
		Mouseup: 'Mouseup'
	} as const;
	export type ButtonMouseState = (typeof ButtonMouseState)[keyof typeof ButtonMouseState];
</script>

<script lang="ts">
	let {
		children,
		ref = $bindable(null),
		mouseState = $bindable('Mouseleave'),
		icon = undefined,
		iconPosition = 'front',
		...rest
	}: ButtonProps & { children?: Snippet } & HTMLButtonAttributes = $props();
</script>
