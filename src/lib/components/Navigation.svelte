<script>
	import { page } from '$app/stores';
</script>

<nav>
	<ul>
		<li><a href="/" class:active={$page.url.pathname === '/'}>Home</a></li>
		<li><a href="/todo" class:active={$page.url.pathname === '/todo'}>Todo</a></li>
	</ul>
</nav>

<style>
	a {
		text-decoration: none;
		color: black;
	}

	ul {
		list-style: none;
		display: flex;
		gap: 8px;
	}

	.active {
		border-bottom: 2px solid black;
	}
</style>
