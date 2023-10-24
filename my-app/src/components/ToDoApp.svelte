<script>
	import { onMount } from 'svelte';
	import ToDoControls from './ToDoControls.svelte';
	import ToDoIteam from './ToDoIteam.svelte';

	let items = [];
	let id = 0;


	onMount(() => {
		if (localStorage.key('items')){
			items = JSON.parse(localStorage.getItem('items'));
		}
		if(items.length) {
		items.forEach((i) =>{
			if(id < i.id) {
				id = i.id;
			}
		});
		id++;
	}
	});

	function onChangeStatus(event) {
		const item = items.find((i) => i.id === event.detail.id);
		item.isDone = !item.isDone;
		items = items;
		localStorage.setItem('items', JSON.stringify(items));
	}

	function onAddItem(event) {
		const item = {
			id: id++,
			text: event.detail.text,
			isDone: false
		};
		items.push(item);
		items = items;
		localStorage.setItem('items', JSON.stringify(items));
	}

	function onDeleteItem(event) {
		const idx = items.findIndex((i) => i.id === event.detail.id);
		items.splice(idx, 1)
		items = items;
		localStorage.setItem('items', JSON.stringify(items));
	}
</script>

<div class="todo-app">
	<ToDoControls on:add={onAddItem}/>
	<div class="todo-app-fieled">
		{#each items as item}
			<ToDoIteam id={item.id} text={item.text} isDone={item.isDone} on:change={onChangeStatus} on:remove={onDeleteItem}/>
		{/each}
	</div>
</div>

<style>
	.todo-app {
		width: 640px;
		height: 640px;
		background: rgb(192, 189, 189);
		border-radius: 60px;
		padding: 40px;
		display: flex;
		flex-direction: column;
		gap: 10px;
	}
	.todo-app-fieled {
		background: white;
		flex-grow: 1;
		border-radius: 60px;
		overflow-y: auto;
		padding: 40px;
	}
</style>
