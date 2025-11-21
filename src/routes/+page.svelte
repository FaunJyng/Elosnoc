<style></style>

<ButtonGroup direction="row">
	<Button
		mode="ingroup"
		onclick={() => {
			console.log('Go Home');
		}}
	>
		Home
	</Button>
	<Button mode="ingroup">Blog</Button>
</ButtonGroup>

<script module>
</script>

<script>
	import Button from '$lib/components/control/button/Button.svelte';
	import ButtonGroup from '$lib/components/control/button/ButtonGroup.svelte';
</script>
