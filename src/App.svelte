<script>
  import { v4 as uuidv4 } from 'uuid';
  
  let todoText = "";
  let todoItems = [];
  let doneItems = [];

  function addTodo() {
    const todo = {
      text: todoText,
      date: new Date().toLocaleString("en-IE"),
    };
    todoItems.push(todo);
    todoItems = [...todoItems];
    todoText = "";
  }

  const todo = {
    text: todoText,
    date: new Date().toLocaleString("en-IE"),
    id: uuidv4()
  };

  function markTodo(id) {
    const found = todoItems.findIndex((todo) => todo.id == id);
    const done = todoItems[found];
    todoItems.splice(found, 1);
    todoItems = [...todoItems];
    doneItems.push(done);
    doneItems = [...doneItems];
  }

  function deleteTodo(id) {
    const found = doneItems.findIndex((todo) => todo.id == id);
    const done = doneItems[found];
    doneItems.splice(found, 1);
    doneItems = [...doneItems];
  }

</script>


<div class="container">
  <div class="box has-text-centered">
    <div class="title"> Simple Todo List</div>
    <div class="subtitle">Fun things to do</div>
  </div>
  <div class="section box">
    <div class="field is-horizontal">
      <div class="field-label is-normal">
        <label for="todo" class="label">What should I do?</label>
      </div>
      <div class="field-body">
        <div class="field">
          <p class="control">
            <input bind:value={todoText} id="todo" class="input" type="text" placeholder="Type something...">
          </p>
        </div>
        <button on:click={addTodo} class="button">Add Todo</button>
      </div>
    </div>
  </div>
  <div class="section box">
    <div class="title is-6">Things yet do</div>
    <table class="table is-fullwidth">
      <thead>
        <th>Task</th>
        <th>Date</th>
        <th>Action</th>
      </thead>
      <tbody>
        {#each todoItems as todo}
          <tr>
            <td> {todo.text} </td>
            <td> {todo.date} </td>
            <td>
              <button on:click={markTodo(todo.id)} class="button">Mark Done</button>
            </td>
          </tr>
        {/each}
      </tbody>
    </table>
  </div>
  <div class="section box">
    <div class="title is-6">Things Done</div>
    <table class="table is-fullwidth">
      <thead>
        <th>Task</th>
        <th>Date</th>
        <th>Action</th>
      </thead>
      <tbody>
        {#each doneItems as todo}
          <tr>
            <td> {todo.text} </td>
            <td> {todo.date} </td>
            <td>
              <button on:click={deleteTodo(todo.id)} class="button">Delete</button>
            </td>
          </tr>
        {/each}
      </tbody>
    </table>
  </div>
</div>