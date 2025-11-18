<style>
	button {
		display: flex;
		flex-direction: column;
		align-items: flex-start;
	}

	.content-area {
		padding: 0 16px;
		line-height: var(--line-height);
	}

	.mid-area,
	.top-area,
	.bot-area {
		display: flex;
		width: 100%;
		align-items: center;
		justify-content: space-between;
	}
</style>

{#snippet main()}
	<div class="top-area">
		<DownRightLine down={{ weight: 'bold' }} />
		<HLine width={contentClientWidth} />
		<DownLeftLine />
	</div>
	<div class="mid-area">
		<VLine height={contentClientHeight} weight="bold" />
		<p bind:this={content} class="content-area">
			{label}
		</p>
		<VLine height={contentClientHeight} />
	</div>
	<div class="bot-area">
		<UpRightLine up={{ weight: 'bold' }} right={{ weight: 'bold' }} />
		<HLine weight="bold" width={contentClientWidth} />
		<UpLeftLine left={{ weight: 'bold' }} />
	</div>
{/snippet}

<button {...handlers}>
	{@render main()}
</button>

<script module>
	export type ButtonProps = {
		label: string;
		handlers?: SvelteMouseEvent<HTMLButtonElement>;
	};
</script>

<script lang="ts">
	import { onMount } from 'svelte';
	import type { SvelteMouseEvent } from '$lib/utils/svelte-mouse-event.js';
	import HLine from '$lib/components/svg/HorizontalLine.svelte';
	import VLine from '$lib/components/svg/VerticalLine.svelte';
	import DownRightLine from '$lib/components/svg/DownRightLine.svelte';
	import DownLeftLine from '$lib/components/svg/DownLeftLine.svelte';
	import UpRightLine from '$lib/components/svg/UpRightLine.svelte';
	import UpLeftLine from '$lib/components/svg/UpLeftLine.svelte';

	let { label, handlers }: ButtonProps = $props();
	let content: HTMLParagraphElement;
	let contentClientWidth: number = $state.raw(0);
	let contentClientHeight: number = $state.raw(0);

	onMount(() => {
		contentClientWidth = content.clientWidth;
		contentClientHeight = content.clientHeight;
	});
</script>
