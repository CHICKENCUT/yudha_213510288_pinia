<template>
  <nav>
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </nav>
  <router-view/>
  <header>
      <h1>YUDHA MART</h1>
    </header>

    <div class="new-task-form">
      <TaskForm/>
    </div>

    <nav class="filter">
      <button @click="filter = 'all'">ALL</button>
      <button @click="filter = 'favs'">BORED</button>
    </nav>
    
    <div class="task-list" v-if="filter === 'all'">
      <p>YOU HAVE {{ taskStore.tasks.length }} SHOPPING </p>
      <div v-for="task in taskStore.tasks" :key="task.id">
        <TaskDetails :task="task"/>
      </div>
    </div>
    <div class="task-list" v-if="filter === 'favs'">
      <p>YOU HAVE {{ taskStore.favs.length }} SHOPPING FAVORITE</p>
      <div v-for="task in taskStore.favs" :key="task.id">
        <TaskDetails :task="task"/>
      </div>
    </div>
</template>
<script>
import { ref } from 'vue';
import TaskDetails from './components/TaskDetails.vue';
import TaskForm from './components/TaskForm.vue';
import { useTaskStore } from './stores/TaskStore';

export default {
  components: { TaskDetails, TaskForm },
  setup() {
    const taskStore = useTaskStore();
    const filter = ref('all');

    return { taskStore, filter };
  },
};
</script>
<style>
  /* Global styles */
  body {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #333333;
    margin: 0;
    padding: 0;
  }

  /* Navigation styles */
  nav {
    background-color: #f8f8f8;
    padding: 20px;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  nav a {
    font-weight: bold;
    color: #614ad3;
    text-decoration: none;
    margin-right: 10px;
    transition: color 0.3s ease;
  }

  nav a:hover {
    color: #9068d6;
  }

  nav a.router-link-exact-active {
    color: #9068d6;
  }

  /* Header styles */
  header {
    background-color: #614ad3;
    color: #ffffff;
    padding: 20px;
  }

  h1 {
    font-size: 36px;
    margin: 0;
  }

  /* Task form styles */
  .new-task-form {
    margin-top: 30px;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  /* Filter styles */
  .filter {
    margin-top: 20px;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .filter button {
    background-color: #614ad3;
    color: #ffffff;
    padding: 10px 20px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    margin-right: 10px;
    transition: background-color 0.3s ease;
  }

  .filter button:focus {
    outline: none;
  }

  .filter button:hover {
    background-color: #9068d6;
  }

  /* Task list styles */
  .task-list {
    margin-top: 30px;
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .task-list p {
    font-weight: bold;
    margin: 0;
    color: #614ad3;
  }

  .task-list div {
    background-color: #f8f8f8;
    padding: 10px;
    margin-top: 10px;
    border-radius: 4px;
    width: 300px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }

  .task-list div:last-child {
    margin-bottom: 10px;
  }
</style>

