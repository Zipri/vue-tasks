<template>
  <li>
    <span v-bind:class="{done: task.completed}">
      <input type="checkbox"
             v-on:change="task.switchCompleteTask()">
      <strong>{{task.id}}</strong>
      {{task.text}}
    </span>
    <button>&times;</button>
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
  border: .01rem dotted #2b2b2b;
  display: flex;
  justify-content: space-between;
  padding: .5rem 2rem;
  margin-bottom: 1rem;
}
li button {
  margin-left: 2rem;
  background-color: white;
  border:  .01rem solid red;
  border-radius: 33%;
  cursor: pointer;
}
li button:hover {
  background-color: red;
  color: white;
}

li input {
  margin-right: 1rem;
}

.done {
  text-decoration: line-through;
}
</style>