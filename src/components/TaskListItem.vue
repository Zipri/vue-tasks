<template>
  <li @click="task.switchCompleteTask()">
    <span v-bind:class="{done: task.completed}">
      {{task.text}}
    </span>
    <button v-on:click="$emit('remove-task', task.id)">&times;</button>
  </li>
</template>
<!-- x === &times; -->

<script>
export default {
  props: {
    task: {
      type: Object,
      required: true, // Если объект не передан - компонента не будет работать
    }
  },
}
</script>

<style scoped>
li {
  border: .01rem dotted #95999a;
  border-radius: 1rem;
  display: flex;
  justify-content: space-between;
  padding: .5rem 2rem;
  margin-bottom: 1rem;
  text-align: justify;
  cursor: pointer;
}
li:hover {
  border: .01rem solid rebeccapurple;
}
li button {
  margin-left: 2rem;
  background-color: white;
  border:  .01rem solid red;
  border-radius: .5rem;
  cursor: pointer;
}
li button:hover {
  background-color: red;
  color: white;
}
.done {
  text-decoration: line-through;
  color: silver;
}
</style>