<script>
	import { createEventDispatcher } from "svelte";

	export let id;
	export let text;
	export let isDone;

	const dispatch = createEventDispatcher();
</script>

<div class="todo-item" class:todo-item-done={isDone}>
	<input class="todo-item-check" type="checkbox" on:change={dispatch('change', { id })} checked={isDone}/>
	<span class="todo-item-text">{text}</span>
	<button class="todo-item-btn" on:click={dispatch('remove', { id })}>Del</button>
</div>

<style>
	.todo-item {
		display: flex;
		align-items: center;
		justify-content: space-between;
		padding: 15px;
		background: rgb(238, 150, 150);
		border-radius: 60px;
		margin-bottom: 30px;
	}
	.todo-item-done {
		background: rgb(129, 227, 129);
	}
	.todo-item-done .todo-item-text {
		text-decoration: line-through;
	}
	.todo-item-text {
		flex-grow: 1;
	}
	.todo-item-btn {
		border: none;
		border-radius: 10px;
		background-color: rgb(183, 86, 86);
		padding: 10px;
		min-width: 10;
	}
</style>
