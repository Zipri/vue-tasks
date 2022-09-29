<template>
  <div id="app">
    <h1>VUE tasks</h1>
    <hr style="width: 100%"/>
    <Form_AddTask @add-task="addTask"
                  @delete-all-tasks="deleteAllTasks"/>
    <TaskList v-bind:tasks="tasks"
              @remove-task="removeTask"/>
  </div>
</template>
<!-- @remove-task == v-on:remove-task -->

<script>
import TaskList from "@/components/TaskList";
import Form_AddTask from "@/components/Form_AddTask";

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
        createTask(6, "Эта пустыня, апофеоз всех пустынь, растянулась до самого неба, в необозримую бесконечность по всем направлениям — белая, слепящая, обезвоженная и совершенно безликая. Только мутное марево горной гряды призрачно вырисовывалось на горизонте, и еще изредка попадались сухие пучки бес-травы, что приносит и сладкие сны, и кошмары, и смерть. Редкий надгробный камень служил указателем на пути. Узенькая тропа, пробивающая толстую корку солончаков, — вот все, что осталось от старой столбовой дороги, где когда-то ходили фургончики и повозки. С тех пор мир сдвинулся с места. Мир опустел."),
      ]
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos')
        .then(response => response.json())
        .then(json => json.map(i => this.tasks.push(createTask(i.id, i.title))))
  },
  methods: {
    removeTask(id) {
      this.tasks = this.tasks.filter(t => t.id !== id)
    },
    addTask(task) {
      this.tasks.unshift(task)
    },
    deleteAllTasks() {
      this.tasks = []
    }
  },
  components: {Form_AddTask, TaskList}
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
