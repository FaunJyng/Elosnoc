<style></style>

<ButtonGroup layout="column">
	<Button mode="group">
		{#snippet iconNormal()}
			<svg
				style:background-color="transparent"
				xmlns="http://www.w3.org/2000/svg"
				height="20"
				viewBox="0 -960 960 960"
				width="20"
				fill="#000000"
				><path d="M219.27-171.27v-416L480-783.69l260.73 196.65v415.77H550.27v-248.46H409.92v248.46H219.27Z" /></svg
			>
		{/snippet}
		{#snippet iconOnclick()}
			<svg
				style:background-color="transparent"
				xmlns="http://www.w3.org/2000/svg"
				height="20"
				viewBox="0 -960 960 960"
				width="20"
				fill="#ffffff"
				><path d="M219.27-171.27v-416L480-783.69l260.73 196.65v415.77H550.27v-248.46H409.92v248.46H219.27Z" /></svg
			>
		{/snippet}
		Home
	</Button>
	<Button mode="group">Blog</Button>
</ButtonGroup>

<script module>
</script>

<script>
	import Button from '$lib/components/control/button/Button.svelte';
	import ButtonGroup from '$lib/components/control/button/ButtonGroup.svelte';
</script>
