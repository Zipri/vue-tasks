<template>
  <div>
    <ul>
      <TaskListItem v-for="task of tasks"
                    v-bind:task="task"
                    :key="task.id"/>
    </ul>
  </div>
</template>

<script>
import TaskListItem from "@/components/TaskListItem";

export default {
  props: ['tasks'],
  components: {TaskListItem}
}
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>