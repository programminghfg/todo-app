<script>
	import { page } from '$app/stores';
</script>

<nav>
	<ul>
		<!-- Wenn der aktuelle Pfad mit dem Link übereinstimmt, wird dieser hervorgehoben in der Navigation. -->
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
		padding-left: 0;
	}

	.active {
		border-bottom: 2px solid black;
	}
</style>
