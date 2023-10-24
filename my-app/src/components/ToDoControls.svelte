<script>
	import { createEventDispatcher } from "svelte";
	const dispatch = createEventDispatcher();
	let inputValue = '';
	function onClick() {
		if(inputValue.length) {
			dispatch('add', {text: inputValue});
			inputValue = '';
		}
	}
</script>

<div class="todo-controls">
	<input class="todo-controls-input" type="text" bind:value={inputValue}/>
	<button class="todo-controls-btn" on:click={onClick}>Add</button>
</div>

<style>
	.todo-controls {
		display: grid;
		grid-template-columns: 65% 35%;
	}
	.todo-controls-input {
		border: none;
		border-radius: 60px 0 0 60px;
		padding: 20px;
	}
	.todo-controls-btn {
		border: none;
		border-radius: 0 60px 60px 0;
		background: rgb(195, 186, 92);
	}
</style>
