<script>
	// browser kann verwendet werden, um zu überprüfen ob die App im Browser läuft. Tei
	import { browser } from '$app/environment';

	// Speichert den aktuellen Input im Eingabefeld.
	let inputValue = '';

	// Alle Todos werden in diesem Array gespeichert.
	let todos = [];

	// Localstorage wird verwendet, um die Tasks im Browser zu speichern, sodass sie nicht verloren gehen beim Schließen der Website.
	if (browser && localStorage.svelteTodos === undefined) {
		localStorage.svelteTodos = JSON.stringify(todos); //speichern im lokalen Storage
	} else if (browser) {
		// Wenn wir uns im Browser befinden und es schon Todos im Localstorage gibt, dann werden die jetzt geladen.
		todos = JSON.parse(localStorage.svelteTodos);
	}

	// Todos hinzufügen
	const addTodo = () => {
		if (inputValue.length) {
			todos.push({ text: inputValue, status: false });
			todos = todos;
			// Speichert die Todos im localStorage.
			localStorage.svelteTodos = JSON.stringify(todos);
			// Das Eingabefeld leeren.
			inputValue = '';
		}
	};

	// Todos lassen sich hiermit verändern und erneut abspeichern.
	const changeTodo = () => {
		localStorage.svelteTodos = JSON.stringify(todos);
	};

	// Todos können hiermit gelöscht werden.
	const removeTodo = (e, searchElement) => {
		// Die Position des richtigen Todo-Task finden.
		const indexToDelete = todos.indexOf(searchElement);
		// Anschließend den Task aus dem Todos-Array löschen.
		todos.splice(indexToDelete, 1);
		todos = todos;
		// Änderungen auch im Localstorage abspeichern/aktualisieren.
		localStorage.svelteTodos = JSON.stringify(todos);
	};

	// Wenn Enter gedrückt wird, wird ein neuer Todo-Task erstellt.
	const enter = (key) => {
		if (key.charCode === 13) {
			addTodo();
			console.log('enter gedrueckt');
		}
	};

	// Aktualisiert automatisch die Anzahl der verbleibenden Todos.
	$: remaining = todos.filter((t) => !t.status).length;
</script>

<div class="container">
	<div class="heading">
		<h1>Your todos</h1>
		<!-- Zeigt die Anzahl der verbleibenden Todos an. -->
		<p><em>{remaining}</em> remaining</p>
	</div>

	<div class="input">
		<!-- Eingabefeld für Tasks. Werte werden in der Variable inputValue zwischengespeichert. -->
		<input
			class="input-todo"
			type="text"
			bind:value={inputValue}
			on:keypress={enter}
			placeholder="Type something..."
		/>
		<!-- On click wird ein neuer Todo-Task hinzugefügt. -->
		<button on:click={addTodo}>Add</button>
	</div>
	<ul>
		<!-- Alle Todos aus dem Array werden hier gerendert. -->
		{#each todos as todo, i}
			<!-- Je nach Status des Tasks wird die .checked CSS Klasse angezeigt oder nicht. -->
			<li class:checked={todo.status}>
				<!-- Checkmark Häkchen, welches den Status des Tasks repräsentiert. -->
				<input
					type="checkbox"
					bind:checked={todo.status}
					on:click={(e) => (todo.status = !todo.status)}
				/>
				<!-- Textfeld, in welchem der Task-Text dargestellt wird oder man auch den Task aktualisieren kann. -->
				<input class="text" bind:value={todo.text} on:change={changeTodo} />
				<!-- Delete Button löscht den zugehörigen Task. -->
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
