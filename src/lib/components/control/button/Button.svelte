<style>
	button {
		display: flex;
		align-items: center;
		justify-content: center;
		position: relative;
		cursor: pointer;
		background-color: var(--btn-bg-color-default);
		color: var(--btn-color-default);
		border-top-width: var(--btn-tb-width, var(--btn-tb-width-default));
		border-top-style: var(--btn-tb-style, var(--btn-tb-style-default));
		border-top-color: var(--btn-tb-color, var(--btn-tb-color-default));
		/*  */
		border-bottom-width: var(--btn-bb-width, var(--btn-bb-width-default));
		border-bottom-style: var(--btn-bb-style, var(--btn-bb-style-default));
		border-bottom-color: var(--btn-bb-color, var(--btn-bb-color-default));
		/*  */
		border-right-width: var(--btn-rb-width, var(--btn-rb-width-default));
		border-right-style: var(--btn-rb-style, var(--btn-rb-style-default));
		border-right-color: var(--btn-rb-color, var(--btn-rb-color-default));
		/*  */
		border-left-width: var(--btn-lb-width, var(--btn-lb-width-default));
		border-left-style: var(--btn-lb-style, var(--btn-lb-style-default));
		border-left-color: var(--btn-lb-color, var(--btn-lb-color-default));
	}

	.label,
	.icon {
		background-color: transparent;
	}

	.label {
		padding: calc(var(--lh-md) / 3) calc(var(--lh-md) / 1.5);
	}

	.icon {
		display: flex;
		height: -webkit-fill-available;
		align-items: center;
		justify-content: center;
	}

	.icon-with-label {
		padding-left: calc(var(--lh-md) / 2);
		padding-right: calc(var(--lh-md) / 2);
	}

	.icon-front {
		border-right: 1px solid;
		border-right-color: var(--icon-rb-color);
	}

	.icon-back {
		border-left: 1px solid;
		border-left-color: var(--icon-lb-color);
	}

	.icon-only {
		padding: calc(var(--lh-md) / 2) calc(var(--lh-md) / 1.5);
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
		style:--btn-bg-color-default="var(--btn-{style}-bg-{mouseState})"
		style:--btn-color-default="var(--btn-{style}-fg-{mouseState})"
		style:--btn-tb-width-default="var(--btn-{style}-tb-width-{mouseState})"
		style:--btn-tb-style-default="solid"
		style:--btn-tb-color-default="var(--btn-{style}-bm-color-{mouseState})"
		style:--btn-bb-width-default="var(--btn-{style}-bb-width-{mouseState})"
		style:--btn-bb-style-default="solid"
		style:--btn-bb-color-default="var(--btn-{style}-bm-color-{mouseState})"
		style:--btn-rb-width-default="var(--btn-{style}-rb-width-{mouseState})"
		style:--btn-rb-style-default="solid"
		style:--btn-rb-color-default="var(--btn-{style}-bm-color-{mouseState})"
		style:--btn-lb-width-default="var(--btn-{style}-lb-width-{mouseState})"
		style:--btn-lb-style-default="solid"
		style:--btn-lb-color-default="var(--btn-{style}-bm-color-{mouseState})"
	>
		<!-- svelte-ignore a11y_no_static_element_interactions -->
		<div
			class="overlay"
			onmousedown={() => (mouseState = ButtonMouseState.mousedown)}
			onmouseup={() => (mouseState = ButtonMouseState.mouseup)}
			onmouseleave={() => (mouseState = ButtonMouseState.mouseleave)}
			onmouseenter={() => (mouseState = ButtonMouseState.mouseenter)}
		></div>
		{#if children && !iconNormal}
			<!-- Label + No icon -->
			<div class="label">
				{@render children()}
			</div>
		{:else if iconNormal && !children}
			<!-- No label + Icon -->
			{#if iconOnclick && mouseState === ButtonMouseState.mousedown}
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
				<div
					class={['icon', 'icon-with-label', 'icon-back']}
					style:--icon-lb-color="var(--btn-{style}-bi-color-{mouseState})"
				>
					{#if iconOnclick && mouseState === ButtonMouseState.mousedown}
						{@render iconOnclick()}
					{:else}
						{@render iconNormal()}
					{/if}
				</div>
			{:else}
				<div
					class={['icon', 'icon-with-label', 'icon-front']}
					style:--icon-rb-color="var(--btn-{style}-bi-color-{mouseState})"
				>
					{#if iconOnclick && mouseState === ButtonMouseState.mousedown}
						{@render iconOnclick()}
					{:else}
						{@render iconNormal()}
					{/if}
				</div>
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
		mouseenter: 'mouseenter',
		mouseleave: 'mouseleave',
		mousedown: 'mousedown',
		mouseup: 'mouseup',
	} as const;
	export type ButtonMouseState = (typeof ButtonMouseState)[keyof typeof ButtonMouseState];

	export type ButtonMode = 'group' | 'normal';

	export type ButtonStyle = 'primary' | 'secondary' | 'ghost' | 'disabled';

	export interface ButtonCustomProps {
		instance?: HTMLButtonElement;
		iconNormal?: Snippet;
		iconOnclick?: Snippet;
		children?: Snippet;
		style?: ButtonStyle;
		iconPosition?: 'front' | 'back';
		mouseState?: ButtonMouseState;
		mode?: ButtonMode;
	}

	export type ButtonProps = ButtonCustomProps & HTMLButtonAttributes;
</script>

<script lang="ts">
	let {
		instance = $bindable(),
		iconNormal = undefined,
		iconOnclick = undefined,
		children = undefined,
		style = 'primary',
		iconPosition = 'front',
		mouseState = ButtonMouseState.mouseleave,
		mode = 'normal',
		...htmlButtonAttributes
	}: ButtonProps = $props();

	if (mode === 'group') {
		getButtonGroupContext().push({
			instance,
			iconNormal,
			iconOnclick,
			mouseState,
			iconPosition,
			mode,
			children,
			...htmlButtonAttributes,
		});
	}
</script>
