<template>
  <h1>Todo list fendi </h1>
  <div>
    <input v-model="newTodo" placeholder="Masukkan Kegiatan">
    <button @click="addTodo">Tambah Kegiatan</button>
    <br><br>
    <button @click="hideCompleted = !hideCompleted">{{ hideCompleted ? 'Tampilkan Semua' : 'Sembunyikan yang sudah selesai' }}</button>
    <ul>
      <li v-for="todo in visibleTodos" :key="todo.id">
        <span :class="{ 'completed': todo.completed }" @click="toggleComplete(todo)">{{ todo.text }}</span>
        <button v-if="!todo.completed" @click="completeTodo(todo.id)">Selesai</button>
        <button v-if="todo.completed" @click="unCompleteTodo(todo.id)">Belum Selesai</button>
        <button @click="removeTodo(todo.id)">Hapus</button>
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
/* CSS untuk membuat background gradient */
body {
  height: 100vh;
  width: 100vw;
  background: linear-gradient(to right, #56ccf2, #2f80ed);
}

/* CSS untuk membuat judul */
h1 {
  font-size: 36px;
  margin-bottom: 20px;
  color: #fff;
}

/* CSS untuk membuat input todo */
input {
  padding: 10px;
  border-radius: 5px;
  border: none;
  background-color: #f7f7f7;
  margin-right: 10px;
  width: 60%;
  font-size: 16px;
}

/* CSS untuk membuat tombol tambah todo */
button:first-of-type {
  padding: 10px 20px;
  border-radius: 5px;
  border: none;
  background-color: #27ae60;
  color: #fff;
  cursor: pointer;
  font-size: 16px;
  transition: all 0.3s ease-in-out;
}

button:first-of-type:hover {
  background-color: #219351;
}

/* CSS untuk membuat tombol tampilkan/sembunyikan todo yang sudah selesai */
button:last-of-type {
  padding: 10px 20px;
  border-radius: 5px;
  border: none;
  background-color: #f39c12;
  color: #fff;
  cursor: pointer;
  font-size: 16px;
  transition: all 0.3s ease-in-out;
}

button:last-of-type:hover {
  background-color: #d98d12;
}

/* CSS untuk membuat daftar todo */
ul {
  list-style: none;
  padding: 0;
  margin-top: 20px;
}

li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 10px;
  padding: 10px;
  border-radius: 5px;
  box-shadow: 0px 2px 10px rgba(0, 0, 0, 0.1);
  background-color: #fff;
}

/* CSS untuk membuat todo yang sudah selesai */
.completed {
  text-decoration: line-through;
  color: #aaa;
}

/* CSS untuk membuat tombol selesai */
button:nth-of-type(2) {
  padding: 5px 10px;
  border-radius: 5px;
  border: none;
  background-color: #27ae60;
  color: #fff;
  cursor: pointer;
  font-size: 16px;
  transition: all 0.3s ease-in-out;
}

button:nth-of-type(2):hover {
  background-color: #219351;
}

/* CSS untuk membuat tombol belum selesai */
button:nth-of-type(3) {
  padding: 5px 10px;
  border-radius: 5px;
  border: none;
  background-color: #e74c3c;
  color: #fff;
  cursor: pointer;
  font-size: 16px;
  transition: all 0.3s ease-in-out;
}

button:nth-of-type(3):hover {
  background-color: #d74434;
}

/* CSS untuk membuat tombol hapus */
button:last-of-type {
  padding: 5px 10px;
  border-radius: 5px;
  border: none;
  background-color: #c0392b;
  color: #fff;
  cursor: pointer;
 

  }</style>