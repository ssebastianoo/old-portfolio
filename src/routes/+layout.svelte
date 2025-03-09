<script lang="ts">
	import '@fontsource-variable/inter';
	import '../app.css';
	let { children } = $props();
</script>

<main class="p-7">
	{@render children()}

	<div
		class="absolute top-20 left-20 -z-10 h-100 max-h-[calc(90%-1rem)] w-100 max-w-[calc(90%-1rem)] -translate-x-1/2 -translate-y-1/2 bg-neutral-600 opacity-50 blur-[300px]"
	></div>
</main>
