<style>
	button {
		display: flex;
		align-items: center;
		justify-content: center;
		border-top: solid var(--primary-foreground);
		border-right: solid var(--primary-foreground);
		border-left: solid var(--primary-foreground);
		border-bottom: solid var(--primary-foreground);
		position: relative;
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
	}

	.icon-with-label {
		padding-left: calc(var(--line-height) / 1.5);
		padding-right: calc(var(--line-height) / 1.5);
	}

	.icon-front {
		border-right: 1px solid var(--primary-foreground);
	}

	.icon-back {
		border-left: 1px solid var(--primary-foreground);
	}

	.icon-only {
		padding: calc(var(--line-height) / 2) calc(var(--line-height) / 1.5);
	}

	.overlay {
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background-color: transparent;
	}
</style>

{#if mode === 'normal'}
	<button
		{...htmlButtonAttributes}
		style:background-color={mouseState === ButtonMouseState.Mousedown
			? 'var(--primary-hover)'
			: 'var(--primary)'}
		style:color={mouseState === ButtonMouseState.Mousedown
			? 'var(--primary-foreground-hover)'
			: 'var(--primary-foreground)'}
		style:border-top-width={mouseState === ButtonMouseState.Mouseenter ||
		mouseState === ButtonMouseState.Mouseup
			? `${border?.top?.widthOnhover}px`
			: `${border?.top?.widthNormal}px`}
		style:border-bottom-width={mouseState === ButtonMouseState.Mouseenter ||
		mouseState === ButtonMouseState.Mouseup
			? `${border?.bottom?.widthOnhover}px`
			: `${border?.bottom?.widthNormal}px`}
		style:border-left-width={mouseState === ButtonMouseState.Mouseenter ||
		mouseState === ButtonMouseState.Mouseup
			? `${border?.left?.widthOnhover}px`
			: `${border?.left?.widthNormal}px`}
		style:border-right-width={mouseState === ButtonMouseState.Mouseenter ||
		mouseState === ButtonMouseState.Mouseup
			? `${border?.right?.widthOnhover}px`
			: `${border?.right?.widthNormal}px`}
	>
		<!-- svelte-ignore a11y_no_static_element_interactions -->
		<div
			class="overlay"
			onmousedown={() => (mouseState = ButtonMouseState.Mousedown)}
			onmouseup={() => (mouseState = ButtonMouseState.Mouseup)}
			onmouseleave={() => (mouseState = ButtonMouseState.Mouseleave)}
			onmouseenter={() => (mouseState = ButtonMouseState.Mouseenter)}
		></div>
		{#if children && !iconNormal}
			<!-- Label + No icon -->
			<div class="label">
				{@render children()}
			</div>
		{:else if iconNormal && !children}
			<!-- No label + Icon -->
			{#if iconOnclick && mouseState === ButtonMouseState.Mousedown}
				<div class={['icon', 'icon-only']}>
					{@render iconOnclick()}
				</div>
			{:else}
				<div class={['icon', 'icon-only']}>
					{@render iconNormal()}
				</div>
			{/if}
		{:else if children && iconNormal}
			<!-- Label + Icon -->
			{#if iconPosition === 'back'}
				<div class="label">
					{@render children()}
				</div>
				{#if iconOnclick && mouseState === ButtonMouseState.Mousedown}
					<div
						class={['icon', 'icon-with-label', 'icon-back', 'icon-only']}
						style:border-left-color={mouseState === ButtonMouseState.Mousedown
							? 'var(--primary-foreground-hover)'
							: 'var(--primary-foreground)'}
					>
						{@render iconOnclick()}
					</div>
				{:else}
					<div
						class={['icon', 'icon-with-label', 'icon-back']}
						style:border-left-color={mouseState === ButtonMouseState.Mousedown
							? 'var(--primary-foreground-hover)'
							: 'var(--primary-foreground)'}
					>
						{@render iconNormal()}
					</div>
				{/if}
			{:else}
				{#if iconOnclick && mouseState === ButtonMouseState.Mousedown}
					<div
						class={['icon', 'icon-with-label', 'icon-front']}
						style:border-right-color={mouseState === ButtonMouseState.Mousedown
							? 'var(--primary-foreground-hover)'
							: 'var(--primary-foreground)'}
					>
						{@render iconOnclick()}
					</div>
				{:else}
					<div
						class={['icon', 'icon-with-label', 'icon-front']}
						style:border-right-color={mouseState === ButtonMouseState.Mousedown
							? 'var(--primary-foreground-hover)'
							: 'var(--primary-foreground)'}
					>
						{@render iconNormal()}
					</div>
				{/if}
				<div class="label">
					{@render children?.()}
				</div>
			{/if}
		{/if}
	</button>
{/if}

<script module>
	import type { HTMLButtonAttributes } from 'svelte/elements';
	import { type Snippet } from 'svelte';
	import { getButtonGroupContext } from './ButtonGroup.svelte';

	export const ButtonMouseState = {
		Mouseenter: 'Mouseenter',
		Mouseleave: 'Mouseleave',
		Mousedown: 'Mousedown',
		Mouseup: 'Mouseup'
	} as const;
	export type ButtonMouseState = (typeof ButtonMouseState)[keyof typeof ButtonMouseState];

	export type ButtonBorderStyle = Partial<{
		widthNormal: number;
		widthOnhover: number;
		widthOnclick: number;
		style: 'solid' | 'dashed';
	}>;

	export type ButtonBorder = Partial<{
		top: ButtonBorderStyle;
		bottom: ButtonBorderStyle;
		left: ButtonBorderStyle;
		right: ButtonBorderStyle;
	}>;

	export const ButtonBorderDefaultStyle = {
		top: {
			widthNormal: 1,
			widthOnhover: 1,
			style: 'solid'
		},
		bottom: {
			widthNormal: 3,
			widthOnhover: 1,
			style: 'solid'
		},
		left: {
			widthNormal: 3,
			widthOnhover: 1,
			style: 'solid'
		},
		right: {
			widthNormal: 1,
			widthOnhover: 1,
			style: 'solid'
		}
	} as const;

	export type ButtonMode = 'ingroup' | 'normal';

	export interface ButtonCustomProps {
		instance?: HTMLButtonElement;
		iconNormal?: Snippet;
		iconOnclick?: Snippet;
		mouseState?: ButtonMouseState;
		iconPosition?: 'front' | 'back';
		border?: ButtonBorder;
		mode?: ButtonMode;
	}

	export type ButtonProps = ButtonCustomProps & { children?: Snippet } & HTMLButtonAttributes;
</script>

<script lang="ts">
	let {
		instance = $bindable(),
		iconNormal = undefined,
		iconOnclick = undefined,
		mouseState = ButtonMouseState.Mouseleave,
		iconPosition = 'front',
		border = ButtonBorderDefaultStyle,
		mode = 'normal',
		children = undefined,
		...htmlButtonAttributes
	}: ButtonProps = $props();

	if (mode === 'ingroup') {
		getButtonGroupContext().push({
			instance,
			iconNormal,
			iconOnclick,
			mouseState,
			iconPosition,
			border,
			mode,
			children,
			...htmlButtonAttributes
		});
	}
</script>
