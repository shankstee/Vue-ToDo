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
      <div v-for="(todo, index) in todos" :key="todo.id" class="todo-item">
        <p>
         <input type="checkbox">
          {{todo.title}}
        </p>
        <button @click="removeTodo(index)">X</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "todo-list",
  data() {
    return {
      newTodoText: "",
      todos: []
    };
  },

    // on page load grab the user todos from local storage
   beforeMount() {
      this.getTodos();
    },
    

  methods: {
    getTodos() {
      let userTodos = localStorage.getItem("userTodos");
      //convert local storage to an JSON obj
      let userTodoObj = JSON.parse(userTodos);
      this.todos = userTodoObj;
      
    },
    

    addTodo() {
        // Validation check
      if (this.newTodoText.trim().length === 0) {
        return;
      }
        // Check if already exists
      if (localStorage.getItem("userTodos") === null) {
          localStorage.setItem("userTodos", JSON.stringify([]));
          
      }

        // this is the users local storage string of info
      let userTodos = localStorage.getItem("userTodos");
      // take said info and parse it into a JSON object
      let userTodoObj = JSON.parse(userTodos);
      //set said JSON obj as the current todo array within data() {}
      this.todos = userTodoObj;

      // push the new To do into said array
      this.todos.push({
        title: this.newTodoText,
        completed: false
      });
      // remove the old userTodo item from local strorage 
      localStorage.removeItem('userTodos');
        // send the new JSON "strin" obj to local storage
      localStorage.setItem("userTodos", JSON.stringify(this.todos));
      // clear the input state
      this.newTodoText = "";
      
    },

    removeTodo(index) {
      //delete the index
        this.todos.splice(index, 1);
        // update local storage
        localStorage.setItem("userTodos", JSON.stringify(this.todos));
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
