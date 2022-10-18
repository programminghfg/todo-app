<script>
	import { browser } from '$app/environment';

	let inputValue = '';

	let todos = [];

	if (browser && localStorage.svelteTodos === undefined) {
		localStorage.svelteTodos = JSON.stringify(todos); //speichern im lokalen Storage
	} else if (browser) {
		todos = JSON.parse(localStorage.svelteTodos);
	}

	const addTodo = () => {
		if (inputValue.length) {
			todos.push({ text: inputValue, status: false });
			todos = todos;
			localStorage.svelteTodos = JSON.stringify(todos);
			inputValue = '';
		}
	};

	const changeTodo = () => {
		localStorage.svelteTodos = JSON.stringify(todos);
	};

	const removeTodo = (e, searchElement) => {
		const indexToDelete = todos.indexOf(searchElement);
		todos.splice(indexToDelete, 1);
		todos = todos;
		localStorage.svelteTodos = JSON.stringify(todos);
	};

	const enter = (key) => {
		if (key.charCode === 13) {
			addTodo();
			console.log('enter gedrueckt');
		}
	};

	$: remaining = todos.filter((t) => !t.status).length;
</script>

<div class="container">
	<div class="heading">
		<h1>Your todos</h1>
		<p><em>{remaining}</em> remaining</p>
	</div>

	<div class="input">
		<input
			class="input-todo"
			type="text"
			bind:value={inputValue}
			on:keypress={enter}
			placeholder="Type something..."
		/>
		<button on:click={addTodo}>Add</button>
	</div>
	<ul>
		{#each todos as todo, i}
			<li class:checked={todo.status}>
				<input
					type="checkbox"
					bind:checked={todo.status}
					on:click={(e) => (todo.status = !todo.status)}
				/>
				<input class="text" bind:value={todo.text} on:change={changeTodo} />
				<button class="button-delete" on:click={(e) => removeTodo(e, todo)}>Delete</button>
			</li>
		{/each}
	</ul>
</div>

<style>
	.input {
		width: 100%;
		display: flex;
		gap: 12px;
		align-items: center;
		justify-content: space-between;
		padding: 4px 8px;
	}
	.input-todo {
		width: inherit;
		border: none;
		border-bottom-style: none;
		border-bottom-width: medium;
		border-bottom: 1px solid black;
		outline: none;
	}

	.button-delete {
		position: absolute;
		right: 0;
		margin-right: 4px;
	}

	.text {
		background: none;
		border: none;
		outline: none;
	}

	ul {
		padding-left: 0;
		list-style: none;
		position: relative;
		display: flex;
		flex-direction: column;
		gap: 4px;
	}

	li {
		display: flex;
		gap: 12px;
		align-items: center;
		padding: 4px 8px;
		border-radius: 4px;
	}

	li:hover {
		background-color: rgb(206, 206, 206);
	}

	.checked {
		background: rgb(210, 210, 236);
		opacity: 50%;
	}

	.checked input {
		text-decoration: line-through;
	}

	.heading {
		font-size: 2rem;
		display: inline-flex;
		justify-content: space-between;
		width: 100%;
		align-items: center;
	}
	.heading h1 {
		font-size: inherit;
	}
	.heading p {
		font-size: inherit;
	}

	em {
		color: red;
		font-style: normal;
	}
</style>
