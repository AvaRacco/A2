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

        <input type="radio" name="category" id="notImportant" value="notImportant" bind:group={todoCategory}>
        <label for="notImportant">Not Important</label>


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
                <button type="button" onclick={() => removeItem(index)}>remove</button>
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
        padding-top: 1vw;
    }

    .important {
        background-color: yellow;
    }

    .overdue {
        background-color: tomato;
    }

    .notImportant {
        background-color: green;
    }

</style>