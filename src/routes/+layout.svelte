<script lang="ts">
	import '@fontsource-variable/inter';
	import Intro from '$lib/Intro.svelte';

	import '../app.css';
	let { children } = $props();
</script>

<main class="min-h-dvh p-7">
	<Intro />
	{@render children()}

	<div
		class="absolute top-20 left-20 -z-10 h-100 w-100 max-w-[calc(90%-1rem)] -translate-x-1/2 -translate-y-1/2 bg-neutral-600 opacity-50 blur-[300px]"
	></div>
</main>
