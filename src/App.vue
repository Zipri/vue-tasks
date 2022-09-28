<template>
  <div id="app">
    <h1>VUE tasks</h1>
    <hr style="width: 100%"/>
    <TaskList v-bind:tasks="tasks"/>
  </div>
</template>

<script>
import TaskList from "@/components/TaskList";

export default {
  name: 'App',
  data() {
    return {
      tasks: [
        {id: 1, text: "The quick brown fox jumps over the lazy dog", completed: false},
        {id: 2, text: "Съешь ещё этих мягких французских булок да выпей чаю", completed: false},
        {id: 3, text: "Høj bly gom vandt fræk sexquiz på wc", completed: true},
        {id: 4, text: "В чащах юга жил бы цитрус? Да, но фальшивый экземпляр!", completed: false},
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
