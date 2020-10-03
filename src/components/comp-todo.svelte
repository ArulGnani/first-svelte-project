<div id="todo" in:fade="{{ y:10, dutation: 1000 }}"
    out:fade="{{ y:0, dutation: 1 }}"
>
    <p class={complete === true ? "done" : "" }> 
        { todo.todo } 
    </p>

    <div>

        <button 
            id="completed" 
            on:click={completedTodo(todo.todo)}
        > 
            done 
        </button>

        <button 
            id="close" 
            on:click={deleteTodo(todo.todo)}
        >
            X 
        </button>

    </div>
</div>

<style>
    .done {
        text-decoration: line-through;
    }
    #todo {
        background: rgb(232, 241, 142);
        font-size: 20px;
        border-radius: 4px;
        padding: 5px;
        margin-top: 5px;
        margin-bottom: 10px;
        display: flex;
        align-items: center;
        justify-content: space-evenly;
    }
    
    #todo p {
        margin: 5px;
        margin-left: 50px;
    }

    #todo div {
        margin-left: auto;
    }

    #close {
        outline: none;
        padding: 10px;
        background: red;
        border: none;
        border-radius: 5px;
        color: white;
        transition: transform ease 0.1s;
    }

    #completed {
        outline: none;
        padding: 10px;
        background: rgb(100, 240, 228);
        border: none;
        border-radius: 5px;
        color: black;
        transition: transform ease 0.1s;
    }

    #todo button:hover {
        transform: scale(0.8);
    }
</style>

<script>

    import { createEventDispatcher } from 'svelte'
    import { fade } from 'svelte/transition'

    const dispatch = createEventDispatcher()

    let todo
    let complete

    $: ({ todo, complete } = $$props)

    const deleteTodo = (todo) => dispatch("deleteTodo", todo)

    const completedTodo = (todo) => dispatch("completedTodo", todo)

</script>