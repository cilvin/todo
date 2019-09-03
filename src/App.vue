<template>
  <div class="centerApp">
    <div class="todoWrapper">
      <div>
        <h1>To Do App</h1>
      </div>
      <div>
        <md-field>
          <label>Add ToDo</label>
          <md-input v-model="currentTodo" @keydown.enter="addTodo()"></md-input>
          <span class="md-helper-text">Press Enter to add ToDo</span>
        </md-field>
      </div>
      <hr />
      <div>
        <h2>Tasks to Complete</h2>
      </div>
      <div>
        <ul class="todos">
          <div class="emptyTodos" v-if="todos.length === 0">
            <p>Looks like you are all caught up!</p>
          </div>
          <li v-for="todo in todos" :key="todo.id">
            <div>
              <table>
                <tr>
                  <td>
                    <span class="checkCircle" v-if="todo.completed" @click="undoneTodo(todo)">
                      <md-icon>X</md-icon>
                      <md-tooltip md-direction="bottom">Uncheck ToDo</md-tooltip>
                    </span>
                    <span v-if="todo.completed === false">
                      <input class="checkBox" type="checkbox" v-model="todo.completed" />
                      <md-tooltip md-direction="bottom">Check ToDo</md-tooltip>
                    </span>
                  </td>
                  <td>{{ todo.label }}</td>
                </tr>
              </table>
            </div>
            <div class="editToDos">
              <span @click="removeTodo(todo)" class="deleteButton">
                <md-icon>backspace</md-icon>
                <md-tooltip md-direction="bottom">Delete ToDo</md-tooltip>
              </span>
              <span class="editButton" v-model="todo.editedTodoId" @click="editTodo(todo)">
                <md-icon>create</md-icon>
                <md-tooltip md-direction="bottom">Edit ToDo</md-tooltip>
              </span>
            </div>
            <div  v-if="todo.editedTodoId">
              <md-field>
                <label>Edit ToDo</label>
                <md-input v-model="todo.editedTodo"></md-input>
              </md-field>
              <div class="editDiv">
                <span class="editDone" @click="updateTodo(todo)">
                  <md-icon>done</md-icon>
                  <md-tooltip md-direction="bottom">Apply</md-tooltip>
                </span>
                <span class="abortEdit" v-model="todo.editedTodoId" @click="hideEdit(todo)">
                  <md-icon>clear</md-icon>
                  <md-tooltip md-direction="bottom">Cancel</md-tooltip>
                </span>
              </div>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      currentTodo: "",
      completed: "",
      editedTodoId: "",
      editedTodo: ""
    };
  },
  methods: {
    addTodo() {
      this.todos.push({
        id: this.todos.length,
        label: this.currentTodo,
        completed: false,
        editedTodoId: false
      });
      this.currentTodo = "";
    },
    removeTodo(todo) {
      var index = this.todos.indexOf(todo);
      this.todos.splice(index, 1);
    },
    editTodo(todo) {
      todo.editedTodoId = true;
    },
    hideEdit(todo) {
      todo.editedTodoId = false;
    },
    updateTodo(todo) {
      todo.label = todo.editedTodo;
      todo.editedTodoId = false;
    },
    undoneTodo(todo) {
      todo.completed = false;
    }
  }
};
</script>

<style>
body,
html {
  width: 100%;
  height: 100%;
  font-family: "Roboto", sans-serif;
  padding: 5px;
}

ul {
  margin: 30px 0;
  padding: 0;
}
li {
  padding: 3px;
  margin: 5px 0;
  list-style-type: none;
  font-size: 18px;
  background-color: rgba(0, 0, 0, 0.5);
  border-radius: 3px;
  box-shadow: 0 2px 10px 0 rgba(0, 0, 0, 0.29);
}
h1,
h2 {
  text-align: center;
}
h2 {
  position: relative;
  top: 15px;
}
hr {
  position: relative;
  top: 15px;
  margin-bottom: 15px;
  border: 0.5px solid black;
}
.todoWrapper {
  width: 100%;
  max-width: 700px;
  height: 500px;
  background-color: rgba(132, 177, 235, 0.7);
  padding: 15px;
  border-radius: 4px;
  color: black;
  box-shadow: 0 2px 10px 0 rgba(0, 0, 0, 0.29);
  overflow: scroll;
}
.centerApp {
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
.md-field,
.md-input {
  width: 100%;
  height: 30px;
  border-bottom: 2px solid black;
  background-color: transparent;
  color: black;
  font-size: 18px;
}
.md-field label {
  color: black;
}
.deleteButton {
  cursor: pointer;
  color: #fc440f;
  margin-top: 0px;
  margin-bottom: 0px;
  margin-right: 65px;
  margin-left: 0px;
}
.editButton {
  cursor: pointer;
  color: white;
  margin-top: 0px;
  margin-bottom: 0px;
  margin-right: 20px;
  margin-left: 0px;
}
.checkCircle {
  color: black;
}
.editToDos {
  margin: 5px 0;
  width: 100%;
  display: flex;
  justify-content: flex-end;
}
.editDone {
  color: white;
  cursor: pointer;
  margin-right: 40px;
 
}
.abortEdit {
  color: #fc440f;
  cursor: pointer;
  margin-right: 15px;
  
}

.editDiv {
   display: flex;
  justify-content: flex-end;
}





.md-tooltip {
  color: white;
  background-color: rgba(0, 0, 0, 0.8);
}
.emptyTodos {
  text-align: center;
  background-color: rgba(0, 0, 0, 0.5);
  border-radius: 3px;
  box-shadow: 0 2px 10px 0 rgba(0, 0, 0, 0.29);
  padding: 20px;
}
</style>