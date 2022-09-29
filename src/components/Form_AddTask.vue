<template>
  <div>
    <form @submit.prevent="onSubmit">
      <input type="text" v-model="title" placeholder="Add new task">
      <button type="submit">+</button>
    </form>
    <button @click="deleteAll">&times;</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: ''
    }
  },
  methods: {
    onSubmit() {
      if (this.title.trim()) {
        const newTask = {
          id: Date.now(), text: this.title, completed: false,
          switchCompleteTask: function () {this.completed = !this.completed}
        }
        this.$emit('add-task', newTask)
        this.title = ''
      } else {
        alert('Wrong task')
      }
    },
    deleteAll() {
      this.$emit('delete-all-tasks')
    }
  }
}
</script>

<style scoped>
div {
  display: inline-flex;
  justify-content: center;
  width: 100%;
  padding: 1rem 0;
}
form {
  width: 70%;
  display: flex;
  justify-content: center;
}

input {
  outline: none;
  width: 100%;
  margin-right: 1rem;
  padding: .5rem;
  border-radius: 1rem;
  border: .1rem solid #c0c0c0;
}

input:hover {
  border: .1rem solid rebeccapurple;
}

input:focus {
  border: .1rem solid rebeccapurple;
}

button {
  margin-left: 1rem;
  padding: 0 .6rem;
  font-size: 1.5rem;
  cursor: pointer;
  border-radius: .8rem;
  border: .1rem solid red;
  background-color: white;
}
button:hover {
  border: .1rem solid red;
  background-color: red;
  color: white;
}
form button {
  margin: 0;
  padding: 0 .6rem;
  font-size: 1.5rem;
  cursor: pointer;
  border-radius: .8rem;
  border: .1rem solid rebeccapurple;
  background-color: white;
}
form button:hover {
  border: .1rem solid rebeccapurple;
  background-color: rebeccapurple;
  color: white;
}
</style>