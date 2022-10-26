<script>
	// Globale CSS Styles werden importiert.
	import '$lib/styles/main.css';
	// Navigation Component wird importiert.
	import Navigation from '$lib/components/Navigation.svelte';
</script>

<Navigation />

<main class="grid container">
	<!-- In den Slot werden alle Page-spezifischen Inhalte eingefügt für die jeweilige Route. -->
	<slot />
</main>

<style>
	body,
	html,
	* {
		font-family: 'Open Sans', sans-serif;
	}
</style>
