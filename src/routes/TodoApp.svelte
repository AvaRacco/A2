<script>
    let todoItem = $state('');
    let todoList = $state([]);
    let todoCategory = $state('');


    function addItem(event) {
        // prevent form submission from destroying page
        event.preventDefault();

            // adding todoItem to  todoList
        todoList = [...todoList, {
            text: todoItem,
            done: false,
            category: todoCategory
        }];

        // clear todoItem
        todoItem = '';

    }

    function removeItem(index) {
        todoList.splice(index,1);
    }

    $inspect(todoList);
</script>


<form onsubmit={addItem}>
    <input type="text" name="todo-item" id="todo-item" bind:value={todoItem}>
        
        <input type="radio" name="category" id="important" value="important" bind:group={todoCategory}>
        <label for="important">Important</label>

        <input type="radio" name="category" id="overdue" value="overdue" bind:group={todoCategory}>
        <label for="overdue">Overdue</label>

        <input type="radio" name="category" id="notUrgent" value="notUrgent" bind:group={todoCategory}>
        <label for="notUrgent">Not Urgent</label>

        <input type="radio" name="category" id="none" value="none" bind:group={todoCategory}>
        <label for="other">No Highlight</label>


    <div>
    <button type="submit">Add Item</button>
    </div>
</form>

<div class="todo-list">
    <ul>
        {#each todoList as item, index}
            <li class="{item.category}">
                <input type="checkbox" bind:checked={item.done}>
                <span class:done={item.done}>{item.text}</span>
                <button type="button" onclick={() => removeItem(index)}>REMOVE</button>
            </li>
        {/each}
    </ul>
</div>


<style>

    .done {
        color: gray;
        text-decoration: line-through;
    }

    ul {
        list-style: none;
        margin: 0;
        padding: 0;
        padding-top: 2vw;

    }

    li {
        padding-top: .6vw;
        padding-bottom: .6vw;
        border-radius: 15px;
        margin-bottom: .6vw;
    }

    .important {
        background-color: rgb(255, 217, 0);
        padding-left: 1vw;
    }

    .overdue {
        background-color: rgb(255, 83, 71);
        padding-left: 1vw;
    }

    .notUrgent {
        background-color: rgb(124, 202, 241);
        padding-left: 1vw;
    }

    .none {
        
        padding-left: 1vw;
    }

    .todo-list {
        button{
            border-radius: 10px;
            margin-left: 1.3vw;
            font-family: "Oswald", sans-serif;
            font-size: 1rem;
        }
    }

</style>