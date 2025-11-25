<style></style>

<div></div>

<script module>
	import { type MatIconName } from './MatIcon.js';
	export type MatIconSize = 'xs' | 'sm' | 'md' | 'lg' | 'xl' | '2xl' | '3xl' | '4xl' | '5xl' | '6xl';

	export interface MatIconProps {
		name: MatIconName;
		size?: MatIconSize;
	}
</script>

<script lang="ts">
	let { name, size = 'md' } = $props();
</script>
