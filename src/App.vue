<template>
  <div id="app">
    <h1>VUE tasks</h1>
    <hr style="width: 100%"/>
    <TaskList v-bind:tasks="tasks"/>
  </div>
</template>

<script>
import TaskList from "@/components/TaskList";

const createTask = (id, text) => {
  return {
    id: id, text: text, completed: false,
    switchCompleteTask: function () {
      this.completed = !this.completed
    }
  }
}

export default {
  name: 'App',
  data() {
    return {
      tasks: [
        createTask(1, "The quick brown fox jumps over the lazy dog"),
        createTask(2, "Съешь ещё этих мягких французских булок да выпей чаю"),
        createTask(3, "Høj bly gom vandt fræk sexquiz på wc"),
        createTask(4, "В чащах юга жил бы цитрус? Да, но фальшивый экземпляр!"),
        createTask(5, "Ехал Грека через реку... а лучше бы не ехал..."),
      ]
    }
  },
  components: {TaskList}
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  display: flex;
  flex-direction: column;
  align-items: center;
}

* {
  transition: .7s; /* Время эффекта */
}
</style>
