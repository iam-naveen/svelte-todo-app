<script lang="ts">
  import src from "./assets/svelte.svg";

  let todoText = "";
  let todoItems = ["Test item 1", "Test item 2", "Test item 3"];

  function addTodo(event) {
    event.preventDefault();
    if (todoText) {
      todoItems.push(todoText);
      todoItems = todoItems;
      todoText = "";
    }
  }

  function removeTodo(item: string) {
    todoItems.splice(todoItems.indexOf(item), 1);
    todoItems = todoItems;
  }

  function checkTodo(event: MouseEvent) {
    const content = (event.target as HTMLDivElement).nextElementSibling;
    content.classList.toggle("line-through");
    content.parentElement.classList.toggle("bg-gray-500");
  }
</script>

<main class="mt-10 ml-10 select-none">
  <img {src} alt="svelte-logo" class="fixed top-3 right-3" />

  <h1 class="text-4xl font-bold">TODO APP</h1>

  <form on:submit={addTodo}>
    <input
      type="text"
      class="bg-cyan-50 outline-none text-black p-2 rounded-sm mt-5"
      bind:value={todoText}
    />
    <input
      type="submit"
      value="Add"
      class="bg-cyan-600 text-black py-2 px-5 rounded-sm mx-2 hover:bg-cyan-400 cursor-pointer"
    />
  </form>

  <div class="todo-items-container w-96">
    {#each todoItems as item}
      <!-- svelte-ignore a11y-click-events-have-key-events -->
      <div
        class="todo-item bg-cyan-500 p-2 rounded-sm mt-5 flex justify-between items-center text-black"
      >
        <input
          type="checkbox"
          class="transform scale-[2] ml-1 cursor-pointer"
          on:click={checkTodo}
        />
        <span class="bg-inherit text-inherit">{item}</span>
        <button
          on:click={removeTodo.bind(this, item)}
          class="bg-cyan-600 px-1 w-5 h-6 rounded select-none">X</button
        >
      </div>
    {/each}
  </div>
</main>
