
<div id="todo">
    
    <AddTodo on:addNewTodo={addNewTodo}/>

    {#if loading}
        <p> loading... </p>
    {/if}

    <AllTodos 
        todos={todos}
        on:deleteTodo={deleteTodo} 
        on:completedTodo={completeTodo}    
    />
</div>

<style>
    #todo {
        width: 70vw;
        margin: auto;
        margin-top: 50px;
        margin-bottom: 100px;
        border: none;
        padding: 10px;
        border-radius: 5px;
        background: greenyellow;
    }
</style>

<script>
    
    import AddTodo from './add-todo.svelte'
    import AllTodos from './all-todos.svelte'
    import { onMount } from 'svelte'

    let todos = []
    let loading = false 

    onMount(async() => {
        loading = true 

        await fetch('https://jsonplaceholder.typicode.com/todos')
            .then(res => res.json())
            .then(data => {
                
                let fetched = []
                let arr = data.splice(0, 50)

                arr.forEach(d => {
                    fetched.push({
                        "todo" : d.title,
                        "complted": d.completed
                    })
                })

                todos = [...fetched]
            })
            .catch(() => alert("something went wrong!.."))
            .finally(() => loading = false)

    })


    const addNewTodo = (newTodo) => {
        todos = [{...newTodo.detail}, ...todos]
    }

    const deleteTodo = (todo) => {
        todos = todos.filter((t) => t.todo != todo.detail)
    }

    const completeTodo = (todo) => {
        todos.forEach(t => {
            if (todo.detail === t.todo) {
                t.completed = true
            }
        })
        todos = [...todos]
    }

</script>