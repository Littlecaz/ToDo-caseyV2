<script>
    import { fly } from 'svelte/transition';
    let todoItem = '';
    let todoList = [];
    // add items from input field to array
    function addToList() {
        if (!todoItem) return;
        todoList = [...todoList, {
            text: todoItem,
            status: false
        }];
        todoItem = '';
    }
    // remove items from array
    function removeFromList(index) {
        todoList.splice(index, 1);
        todoList = todoList;
    }
</script>

<form on:submit|preventDefault={addToList}>
    <input bind:value={todoItem}>
</form>

<div>
<ol class="todo-list">
    {#each todoList as item, index}
    <li transition:fly="{{ y: 20, duration: 200 }}">
    <input bind:checked={item.status} class="checkbox" type="checkbox">
    <span class:checked={item.status}>{item.text}</span>
    <button class="delete" type="button" on:click={() => removeFromList(index)} ></button>
    </li>
    {/each}
</ol>
</div>

<style>
    div {
        padding-left: 2em;
        width: 50%;
        height: 700px;
        position: fixed; 
        top: 25vph;
        left: 25%;
        overflow: scroll;
    }
    .todo-list {
        margin: 2em;
        list-style: none;
        background-color: rgb(255, 240, 190);
        word-wrap: break-word;
    }
    li:nth-child(even) {
        background-color: rgb(255, 255, 255);
    }
    .checked {
        text-decoration: line-through;
        color: crimson;
    }
    .checked + .delete{
        display: block;
    }
    .checkbox {
        display: block;
        top: 1em;
        left: 3px;
        padding-left: 2em;
    }
    .delete {
        display: none;
    }
    span {
        display: block;
        word-break: break-word;
        overflow: hidden;
        padding-left: 1em;
    }
</style>