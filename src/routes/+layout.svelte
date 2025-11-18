<style>
	main {
		display: flex;
		align-items: center;
		justify-content: center;
		min-height: 100vh;
		min-width: 100vw;
	}
</style>

<main>
	{@render children()}
</main>

<script>
	import '$lib/styles/index.css';
	let { children } = $props();
</script>
