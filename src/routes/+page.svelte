<script>
    import { writable } from 'svelte/store';

    let filter = 'all';
    let items = writable(['Task1', 'Task2', 'Task3', 'Task4']);
    let newItem = '';
  
    function addItem() {
      if (newItem.trim()) {
        items.update(currentItems => [...currentItems, newItem]);
        newItem = '';
      }
    }
  
    function deleteItem(index) {
      items.update(currentItems => currentItems.filter((_, i) => i !== index));
    }
  
    function handleKeyPress(event) {
      if (event.key === 'Enter') {
        addItem();
      }
    }
  
    // Sección 2 - Calificación
    let rating = null;
  
    function selectRating(value) {
      rating = value;
    }
  
    function submit() {
      if (rating !== null) {
        console.log(`Calificación enviada: ${rating}`);
      } else {
        alert('Por favor selecciona una calificación.');
      }
    }
  </script>
  
  <header>
    <h1>Todo</h1>
    <div class="theme-black">
      <button class="checkbox" on:click={() => theme.update(t => t === 'dark' ? 'light' : 'dark')}>Bt</button>
    </div>
  </header>
  
  <main>
    <button class="add_button" on:click={addItem}>Agregar</button>
    <input type="text" bind:value={newItem} placeholder="Create new todo...." on:keypress={handleKeyPress} />
  </main>
  
  <section class="section1">
    <ul>
      {#each $items as item, index}
        <li>
          <span class="bt"></span>
          <p class="text">{item}</p>
          <button class="remove" on:click={() => deleteItem(index)}>Click</button>
        </li>
      {/each}
    </ul>

    <div class="bottom-items">
        <div class="item-left"><span>2</span> task</div>
      
        <div class="filter flex-row">
          <label>
            <input type="radio" name="filter" id="all" bind:group={filter} value="all">
            <span>All</span>
          </label>
          <label>
            <input type="radio" name="filter" id="active" bind:group={filter} value="active">
            <span>Active</span>
          </label>
          <label>
            <input type="radio" name="filter" id="completed" bind:group={filter} value="completed">
            <span>Completed</span>
          </label>
        </div>
      
        <span class="clear">Clear completed</span>
      </div>
  </section>
  
  <section class="content-2">
    <div class="container">
      <div class="head">
        <img src="../src/public/images/icon-star.svg" class="icon" alt="Star Icon">
        <h2>How did we do?</h2>
      </div>
  
      <div class="text">
        <p>Please let us know how we did with your support request.
          All feedback is appreciated to help us improve our offering!</p>
      </div>
  
      <div class="button">
        {#each [1, 2, 3, 4, 5] as number}
          <button 
            class="number" 
            class:selected={rating === number} 
            on:click={() => selectRating(number)}
          >
            {number}
          </button>
        {/each}
      </div>
  
      <button class="sub" on:click={submit}>Submit</button>
    </div>
  </section>
  
  
  <footer>
    <h2>Hecho por Johana Usaquen - FrontendMentor</h2>
  </footer>

<style>
    :root {
      --bag-top-image: url("/src/public/images/bg-desktop-dark.jpg");
      --main-bg: hsl(235, 21%, 11%);
      --todo-bg: hsl(235, 24%, 19%);
      --todo-shadow: hsl(235, 21%, 11%);
      --font-color: hsl(234, 39%, 85%);
      --font-color-hover: #FFF;
      --button-bg: hsl(234, 13%, 28%);
      --main-bg-lg: hsl(0, 0%, 98%);
      --todo-bg-lg: hsl(0, 0%, 98%);
      --todo-shadow-lg: hsl(235, 9%, 61%);
      --font-color-lg: hsl(235, 9%, 61%);
      --font-color-hover-lg: hsl(235, 21%, 11%);
      --Orange: hsl(25, 97%, 53%);
      --White: hsl(0, 0%, 100%);
      --Light-Grey: hsl(217, 12%, 63%);
      --Dark-Blue: hsl(213, 19%, 18%);
      --Very-Dark-Blue: hsl(216, 12%, 8%);
}

header{
        display: flex;
        width: 100%;
        max-width: 545px;
        align-items: center;
        justify-content: space-between;
}

button.checkbox{
        background: url('../public/images/icon-moon.svg');
        width: 20px;
        height: 20px;
        color: transparent;
        border: none;
        background-size: cover;
}


main {
      display: flex;
      background: var(--todo-bg);
      width: 100%;
      max-width: 545px;
      padding-block: 20px;
      border-radius: 5px;
}
  
input {
      background: none;
      border: transparent;
      padding: 0 10px;
}
  
.add_button {
      border: 1px solid var(--font-color);
      border-radius: 50px;
      background: transparent;
      color: transparent;
      width: 20px;
      cursor: pointer;
      margin: 0 15px 0 20px;
}
  
.add_button:hover {
      background: center url('../public/images/icon-check.svg') no-repeat,
        linear-gradient(135deg, hsl(192, 100%, 67%), hsl(200, 87%, 65%));
}
  
ul {
      list-style: none;
      padding: 0;
      margin: 0;
}
  
span.bt {
      border: 1px solid var(--font-color);
      width: 20px;
      height: 20px;
      border-radius: 50%;
      margin: 0 20px;
      cursor: pointer;
}
  
span.bt:hover {
      background: center url('../public/images/icon-check.svg') no-repeat,
        linear-gradient(135deg, hsl(192, 100%, 67%), hsl(200, 87%, 65%));
}
  
li {
      display: flex;
      align-items: center;
      padding: 0 10px 0 0px;
      border-bottom: 1px solid var(--font-color);
      position: relative;
      justify-content: flex-start;
}
  
li:hover .remove {
      display: flex;
}
  
button.remove {
      background: url('../public/images/icon-cross.svg');
      width: 18px;
      height: 18px;
      cursor: pointer;
      position: absolute;
      color: transparent;
      right: 25px;
      border: none;
      display: none;
}
  
section.section1 {
      display: flex;
      flex-direction: column;
      background: var(--todo-bg);
      width: 100%;
      max-width: 545px;
      margin-top: 20px;
      border-radius: 5px;
}
  
button.number.selected {
      background-color: var(--Orange);
      color: white;
}
  
.content-2 {
      width: 100%;
      max-width: 545px;
      background: var(--todo-bg);
      border-radius: 5px;
      box-shadow: 0 42px 30px -9px var(--todo-shadow);
      margin: 10% auto;
      padding: 20px;
}
  
.container {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 20px;
}
  
.head {
      padding: 0 15px;
      display: flex;
      align-items: flex-start;
      width: 100%;
      gap: 30px;
      flex-direction: column;
}
  
img.icon {
      background: var(--Light-Grey);
      padding: 12px;
      border-radius: 50%;
      width: 50px;
      height: 50px;
      margin-top: 20px;
}
  
h2 {
      color: var(--font-color);
      font-size: 1.5em;
      margin: 0;
}
  
p {
      padding: 0 15px;
      text-align: center;
}
  
.button {
      display: flex;
      gap: 10px;
      justify-content: center;
}
  
button.number {
      background: var(--Light-Grey);
      border: none;
      border-radius: 50%;
      width: 45px;
      height: 45px;
      cursor: pointer;
      font-size: 16px;
      margin: 0 20px;
}
  
button.number:hover {
      filter: brightness(80%);
}
  
button.sub {
      width: 100%;
      background-color: var(--Orange);
      border: none;
      height: 40px;
      border-radius: 5px;
      color: white;
      font-weight: bold;
      cursor: pointer;
      margin: 20px 0;
}
  
button.sub:hover {
      filter: brightness(80%);
}
  
footer {
      background: var(--Very-Dark-Blue);
      font-size: 6px;
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 10px 0;
      height: 50px;
}

div.bottom-items{
    display: flex;
    padding: 20px;
    justify-content: space-around;
}

  </style>
  