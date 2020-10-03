<div>

    {#each todos as todo}
        <TodoComp 
            todo={todo} 
            complete={todo.completed}
            on:deleteTodo={deleteTodo}
            on:completedTodo={completedTodo}
        />
    {/each}

</div>

<style></style>

<script>

    import TodoComp from './comp-todo.svelte'
    import { createEventDispatcher } from 'svelte'

    const dispatch = createEventDispatcher()

    const deleteTodo = (todo) => dispatch("deleteTodo", todo.detail)
    
    const completedTodo = (todo) => dispatch("completedTodo", todo.detail)

    let todos;
    
    $: ({ todos } = $$props)

</script>