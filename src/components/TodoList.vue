<template>
  <div>
    <input
      type="text"
      class="todo-input"
      placeholder="What needs to be done?"
      v-model="newTodo"
      @keyup.enter="addTodo"
    >
    <div id="todoListDiv">
      <div v-for="todo in todos" :key="todo.id" class="todo-item"><p>{{todo.title}}</p><button>X</button></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "todo-list",
  data() {
    return {
      todoID: 7,
      newTodo: "",
      todos: [
        {
          id: 1,
          title: "Finish Vue Todo list with Vue.js",
          completed: false
        },
        {
          id: 2,
          title: "Check lesson plan for first Sub instructor day.",
          completed: false
        },
        {
          id: 3,
          title: "Work on DB for meeting with emily Wed.",
          completed: false
        },
        {
          id: 4,
          title: "Finish Vue Todo list with Vue.js",
          completed: false
        },
        {
          id: 5,
          title: "Check lesson plan for first Sub instructor day.",
          completed: false
        },
        {
          id: 6,
          title: "Work on DB for meeting with emily Wed.",
          completed: false
        }
      ]
    };
  },

  methods: {
    addTodo() {
      if (this.newTodo.trim().length === 0) {return};  
      this.todos.push({
        id: this.todoID,
        title: this.newTodo,
        completed: false
      });
      this.newTodo = "";
      this.todoID++;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang ="scss">
#todoListDiv {
  /* display: flex;
  flex-wrap: wrap; */
}
.todo-input {
  width: 100%;
  margin: 5px;
  padding: 5px;
}

.todo-item {
  display: flex;
  justify-content: space-between;
  margin: 15px;
  border: solid red 5px;
}

button {
    color: palegreen;
    background: #2c3e50;
}
</style>
