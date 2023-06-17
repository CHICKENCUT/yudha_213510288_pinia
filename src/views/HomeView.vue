<template>
  <h1>To Do List Yudha</h1>
  <div>
    <input v-model="newTodo" placeholder="Masukkan Kegiatan">
    <button @click="addTodo">
Input Activites</button>
    <br><br>
    <button @click="hideCompleted = !hideCompleted">{{ hideCompleted ? 'Hide ALL' : 'Hide done' }}</button>
    <ul>
      <li v-for="todo in visibleTodos" :key="todo.id">
        <span :class="{ 'completed': todo.completed }" @click="toggleComplete(todo)">{{ todo.text }}</span>
        <button v-if="!todo.completed" @click="completeTodo(todo.id)">
finished</button>
        <button v-if="todo.completed" @click="unCompleteTodo(todo.id)">
not finished yet</button>
        <button @click="removeTodo(todo.id)">
wipe</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      todos: [],
      newTodo: '',
      nextId: 1,
      hideCompleted: false
    }
  },
  computed: {
    visibleTodos() {
      if (this.hideCompleted) {
        return this.todos.filter(todo => !todo.completed);
      } else {
        return this.todos;
      }
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() !== '') {
        this.todos.push({
          id: this.nextId++,
          text: this.newTodo,
          completed: false
        });
        this.newTodo = '';
      }
    },
    removeTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id);
    },
    completeTodo(id) {
      const todo = this.todos.find(todo => todo.id === id);
      if (todo) {
        todo.completed = true;
      }
    },
    unCompleteTodo(id) {
      const todo = this.todos.find(todo => todo.id === id);
      if (todo) {
        todo.completed = false;
      }
    },
    toggleComplete(todo) {
      todo.completed = !todo.completed;
    }
  }
}
</script>

<style>
.todo-list {
  margin: 0 auto;
  max-width: 600px;
  font-family: sans-serif;
}

h1 {
  text-align: center;
  font-weight: bold;
  margin-top: 30px;
}

input {
  padding: 10px;
  width: 70%;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 5px;
  margin-bottom: 10px;
}

button {
  padding: 10px 20px;
  margin-left: 10px;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

button:hover {
  background-color: #7188a1;
}

ul {
  padding: 0;
  margin: 0;
}

li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 10px;
  padding: 10px;
  border: 1px solid #6f4343;
  border-radius: 5px;
}

.completed {
  text-decoration: line-through;
  color: gray;
}

button.finished {
  background-color: green;
}

button.finished:hover {
  background-color: darkgreen;
}

button.not-finished {
  background-color: orange;
}

button.not-finished:hover {
  background-color: darkorange;
}

button.wipe {
  background-color: red;
}

button.wipe:hover {
  background-color: darkred;
}
</style>