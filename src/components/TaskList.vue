<template>
  <div>
    <ul>
      <li v-for="(task, index) in tasks" :key="index">
        {{ task.name }} - {{ task.time }} minutes
        <button @click="editTask(task)">Edit</button>
      </li>
    </ul>
    <EditTaskForm :task="selectedTask" @updateTask="updateTask" v-if="showEditForm" />
  </div>
</template>

<script>
import { ref } from 'vue';
import EditTaskForm from './EditTaskForm.vue';

export default {
  props: {
    tasks: Array,
  },
  components: {
    EditTaskForm,
  },
  setup(props, { emit }) {
    const showEditForm = ref(false);
    const selectedTask = ref(null);

    const editTask = (task) => {
      selectedTask.value = {...task};
      showEditForm.value = true;
    };

    const updateTask = (updatedTask) => {
      const index = props.tasks.findIndex(t => t.name === updatedTask.name);
      if (index !== -1) {
        const newTasks = [...props.tasks];
        newTasks[index] = updatedTask;
        showEditForm.value = false;
        emit('updateTasks', newTasks);
      }
    };

    return {showEditForm, selectedTask, editTask, updateTask};
  },
};
</script>
