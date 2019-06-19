<template>
  <div>
    <input
      type="text"
      class="todo-input"
      placeholder="What needs to be done?"
      v-model="newTodoText"
      @keyup.enter="addTodo"
    >
    <div id="todoListDiv">
      <div v-for="(todo) in todos" :key="todo.id" class="todo-item">
        <p>
          <span>{{todo.id}}.</span>
          {{todo.title}}
        </p>
        <button @click="addTodo">X</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "todo-list",
  data() {
    return {
      todoID: 44,
      newTodoText: "",
      todos: []
    };
  },

//    created() {
//     // this.getTodos();
//   },

  methods: {
    getTodos() {
      let userTodos = localStorage.getItem("userTodos");
      //convert local storage to an JSON obj
      let userTodoObj = JSON.parse(userTodos);
      this.todos = userTodoObj;
      
    },
    // beforeMount() {
    //   this.renderLocalStorage();
    // },

    addTodo() {
        // localStorage.removeItem('userTodos');
      if (this.newTodoText.trim().length === 0) {
        return;
      }

        // this is the users local storage string of info
      let userTodos = localStorage.getItem("userTodos");
      // take said info and parse it into a JSON object
      let userTodoObj = JSON.parse(userTodos);
      // set said JSON obj as the current todo array within data() {}
    //   this.todos = userTodoObj;
      console.log(this.todos)
      // push the new To do into said array
      this.todos.push({
        id: this.todoID,
        title: this.newTodoText,
        completed: false
      });
      // remove the old userTodo item from local strorage 
      localStorage.removeItem('userTodos');
      // clear the input state
      this.newTodo = "";
      this.todoID++;
      
        // send the new JSON obj to local storage
      localStorage.setItem("userTodos", JSON.stringify(this.todos));
      
    },

    removeTodo(index) {
      // Read the local storage, save it as a object within a variable
      //delete the index
      console.log("clicked");
      //   this.todos.splice(index, 1);
      localStorage.removeItem("userTodos.[0]");
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
  border: solid #42b883 2px;
  border-radius: 0.25rem;
  padding: 2px;
}

button {
  color: palegreen;
  background: #35495e;
  border-radius: 0.25rem;
}
</style>
