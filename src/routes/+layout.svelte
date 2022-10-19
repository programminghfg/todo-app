<script>
	// Navigation Component wird importiert.
	import Navigation from '$lib/components/Navigation.svelte';
	// Globale CSS Styles werden importiert.
	import '$lib/styles/main.css';
</script>

<Navigation />

<main class="grid container">
	<!-- In den Slot werden alle Page-spezifischen Inhalte eingefügt für die jeweilige Route. -->
	<slot />
</main>
