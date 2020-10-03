<div id="add-todo">

    <input 
        type="text" 
        placeholder="add new todo"
        bind:value={newTodo.todo}
    />
    <button on:click={addTodo}> + </button>

</div>

<style>
    #add-todo {
        /* border: 2px solid fuchsia; */
        margin-top: 20px;
        margin-bottom: 20px;
    }
    #add-todo input {
        outline: none;
        border-radius: 4px;
        border: 2px solid black;
        font-size: 20px;
        padding: 4px;
        width: 88%;
    }
    #add-todo button {
        font-size: 20px;
        padding: 5px;
        border: none;
        border-radius: 4px;
    }
</style>

<script>
    import { createEventDispatcher } from 'svelte'

    const dispatch = createEventDispatcher()

    let newTodo = { "todo" : "", "completed": false }

    const addTodo = () => {
        dispatch("addNewTodo", newTodo)
        newTodo.todo = ""
    }

</script>