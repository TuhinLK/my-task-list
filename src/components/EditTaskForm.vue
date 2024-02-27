<template>
  <div>
    <input type="text" v-model="editedTask.name" placeholder="Task name" /><br />
    <input type="number" v-model.number="editedTask.time" placeholder="Time" /><br />
    <button @click="submit">Submit</button>
  </div>
</template>

<script>
import { ref, watch } from 'vue';

export default {
  props: {
    task: Object,
  },
  setup(props, { emit }) {
    const editedTask = ref({ ...props.task });

    // Watch for changes in the task prop
    watch(() => props.task, (newTask) => {
      editedTask.value = { ...newTask };
    });

    const submit = () => {
      emit('updateTask', editedTask.value);
    };

    return { editedTask, submit };
  },
};
</script>
