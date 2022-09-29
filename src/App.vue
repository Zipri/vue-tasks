<template>
  <div id="app">
    <div class="label">
      <h1>VUE</h1>
      <select v-model="filter">
        <option value="all">All</option>
        <option value="completed">Completed</option>
        <option value="not-completed">Not completed</option>
      </select>
      <h1>tasks</h1>
    </div>
    <hr style="width: 100%"/>
    <Form_AddTask @add-task="addTask"
                  @delete-all-tasks="deleteAllTasks"/>
    <MyLoader v-if="loading"/>
    <TaskList v-else-if="filteredTasks.length"
              v-bind:tasks="filteredTasks"
              @remove-task="removeTask"/>
    <p v-else>- No tasks yet -</p>
  </div>
</template>
<!-- @remove-task == v-on:remove-task -->

<script>
import TaskList from "@/components/TaskList";
import Form_AddTask from "@/components/Form_AddTask";
import MyLoader from "@/components/MyLoader";

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
        createTask(331, "The quick brown fox jumps over the lazy dog"),
        createTask(332, "Съешь ещё этих мягких французских булок да выпей чаю"),
        createTask(333, "Høj bly gom vandt fræk sexquiz på wc"),
        createTask(334, "В чащах юга жил бы цитрус? Да, но фальшивый экземпляр!"),
        createTask(335, "Ехал Грека через реку... а лучше бы не ехал..."),
        createTask(336, "Эта пустыня, апофеоз всех пустынь, растянулась до самого неба, в необозримую бесконечность по всем направлениям — белая, слепящая, обезвоженная и совершенно безликая. Только мутное марево горной гряды призрачно вырисовывалось на горизонте, и еще изредка попадались сухие пучки бес-травы, что приносит и сладкие сны, и кошмары, и смерть. Редкий надгробный камень служил указателем на пути. Узенькая тропа, пробивающая толстую корку солончаков, — вот все, что осталось от старой столбовой дороги, где когда-то ходили фургончики и повозки. С тех пор мир сдвинулся с места. Мир опустел."),
      ],
      loading: true,
      filter: 'all'
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos')
        .then(response => response.json())
        .then(json => {
          json.map(i => this.tasks.push(createTask(i.id, i.title)))
          this.loading = false
        })
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
  computed: {
    filteredTasks() {
      if (this.filter === 'completed') {
        return this.tasks.filter(t => t.completed)
      } else if (this.filter === 'not-completed') {
        return this.tasks.filter(t => !t.completed)
      }
      return this.tasks
    }
  },
  components: {MyLoader, Form_AddTask, TaskList}
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

.label {
  display: flex;
}

.label h1 {
  margin: 0 .5rem;
}

.label select {
  text-align: center;
  outline: none;
  padding: .2rem;
  border-radius: 1rem;
  font-size: 1.25rem;
  cursor: pointer;
  border: .1rem solid rebeccapurple;
  color: rebeccapurple;
  transition: .2s;
}

.label select:hover {
  border: .1rem solid rebeccapurple;
  background-color: rebeccapurple;
  color: white;
}
</style>
