<script>
	import Navigation from '$lib/components/Navigation.svelte';
	import '$lib/styles/main.css';
</script>

<Navigation />

<main class="grid container">
	<slot />
</main>
