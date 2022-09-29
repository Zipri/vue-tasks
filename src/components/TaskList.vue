<template>
  <div>
    <ul>
      <TaskListItem v-for="task of tasks"
                    v-bind:task="task" :key="task.id"
                    v-on:remove-task="removeTask"/>
    </ul>
  </div>
</template>

<script>
import TaskListItem from "@/components/TaskListItem";

export default {
  props: ['tasks'],
  methods: {
    removeTask(id) {
      this.$emit('remove-task', id)
    }
  },
  components: {TaskListItem}
}
</script>

<style scoped>
div {
  padding: 0 3rem;
}
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>