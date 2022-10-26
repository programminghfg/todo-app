<script>
	export let type;
</script>

<button on:click class={type}>
	<slot />
</button>

<style>
	button {
		background: #ff2773;
		border-radius: 24px;
		min-width: 67px;
		height: 36px;
		color: white;
		padding: 8px 16px;
		border: none;
		font-weight: 700;
	}

	.secondary {
		background: #2b1e70;
	}
</style>
