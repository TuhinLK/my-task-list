<template>
  <div>
    <h1>Task List</h1>
    <TaskList :tasks="tasks" @updateTasks="updateTasks" />
  </div>
</template>

<script>
import {ref} from 'vue';
import TaskList from './components/TaskList.vue';

export default {
  components: {
    TaskList,
  },
  setup() {
    const tasks = ref([
      {name: 'Task 1', time: 30},
      {name: 'Task 2', time: 40},
      {name: 'Task 3', time: 60},
      {name: 'Task 4', time: 45},
      {name: 'Task 5', time: 50},
    ]);

    const updateTasks = (newTasks) => {
      tasks.value = newTasks;
    };

    return {tasks, updateTasks};
  },
};
</script>
