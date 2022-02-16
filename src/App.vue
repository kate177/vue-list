<template>
  <div id="app">
    <header>
      <h1 class="title">to do list</h1>
    </header>

    <div class="add-todo-wrapper">
      <div class="input-wrapper">
        <input v-model="todo" type="text" placeholder="Введите задачу" />
      </div>
      <div class="button-wrapper">
        <button @click="addTodo(id++)">Добавить</button>
      </div>
    </div>

    <div class="subtitle">
      <h2 class="objective">Задачи:</h2>
    </div>
    <todo-list
      :todos="todos"
      v-on:remove-todo="removeTodo"
      v-on:btn-complete="complete"
      v-on:btn-check="checkBtn"
    />
  </div>
</template>

<script>
import todoList from "./components/todoList.vue";
export default {
  components: {
    todoList,
  },
  data() {
    return {
      todo: "",
      todos: [],
      isDone: false,
      id: 0,
    };
  },
  mounted() {
    const data = localStorage.getItem("todos");
    data ? (this.todos = JSON.parse(data)) : null;
  },
  methods: {
    addTodo() {
      let now = new Date().toLocaleString();
      if (this.todo != "") {
        this.todos.push({
          id: this.id,
          dates: now,
          text: this.todo,
          isComplete: this.isDone,
        });
        localStorage.setItem("todos", JSON.stringify(this.todos));
      }
      this.todo = "";
    },
    complete(index) {
      this.todos[index].isComplete = !this.todos[index].isComplete;
      if (this.todos[index].isComplete) {
        let btnComplete = document.querySelector(".btn-complete");
        let btnDelete = document.querySelector(".btn-delete");
        let btnCheck = document.querySelector(".btn-check");
        btnComplete.style = "display:none";
        btnDelete.style = "display:none";
        btnCheck.style = "display:block";
      }
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
    checkBtn(index) {
      this.todos[index].isComplete = !this.todos[index].isComplete;
      if (!this.todos[index].isComplete) {
        let btnComplete = document.querySelector(".btn-complete");
        let btnDelete = document.querySelector(".btn-delete");
        let btnCheck = document.querySelector(".btn-check");
        btnComplete.style = "display:block";
        btnDelete.style = "display:block";
        btnCheck.style = "display:none";
      }
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
* {
  padding: 0;
  margin: 0;
  border: 0;
}
*,
*:before,
*:after {
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
}
:focus,
:active {
  outline: none;
}
a:focus,
a:active {
  outline: none;
}
nav,
foother,
header,
aside {
  display: block;
}
html,
body {
  height: 100%;
  width: 100%;
  font-size: 100%;
  line-height: 1;
  font-size: 14px;
  -ms-text-size-adjust: 100%;
  -moz-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
}

button {
  cursor: pointer;
}
button::-moz-focus-inner {
  padding: 0;
  border: 0;
}
a,
a:visited {
  text-decoration: none;
}
a:hover {
  text-decoration: none;
}
ul li {
  list-style: none;
}
img {
  vertical-align: top;
}
h1,
h2,
h3,
h4,
h5,
h6 {
  font-size: inherit;
  font-weight: 400;
}
/*__________________________*/
body {
  width: 100%;
  height: 100%;
  background: rgb(10, 209, 197);
  background: linear-gradient(
    137deg,
    rgba(10, 209, 197, 1) 0%,
    rgba(0, 54, 193, 0.33967090254070376) 100%
  );
  overflow: hidden;
}
.title {
  text-align: center;
  margin-top: 20px;
  font-family: "Montserrat";
  font-weight: bold;
  font-size: 36px;
  line-height: 44px;
  letter-spacing: 0.05em;
  text-transform: uppercase;
  color: #0e5582;
}
.add-todo-wrapper {
  display: flex;
  width: 482px;
  height: 96px;
  margin: 0 auto;
  margin-top: 40px;
  background: #ffffff;
  border-radius: 5px;
  padding: 30px 25px;
  box-shadow: 4px 4px 12px 2px rgba(0, 0, 0, 0.19);
  -webkit-box-shadow: 4px 4px 12px 2px rgba(0, 0, 0, 0.19);
  -moz-box-shadow: 4px 4px 12px 2px rgba(0, 0, 0, 0.19);
}
.input-wrapper {
  width: 294px;
  height: 36px;
  border: 2px solid #4faed5;
  box-sizing: border-box;
  border-radius: 5px;
}
input {
  width: 100%;
  height: 100%;
  padding-left: 14px;
  font-family: "Roboto";
}
.button-wrapper {
  width: 105px;
  height: 36px;
  margin-left: 33px;
}
.button-wrapper button {
  width: 100%;
  height: 100%;
  background: #62abd9;
  border-radius: 5px;
  font-family: "Roboto";
  font-size: 18px;
  line-height: 21px;
  color: #ffffff;
  cursor: pointer;
}
.subtitle {
  margin: 0 auto;
  margin-top: 30px;
  width: 90px;
}
h2 {
  margin: 0 auto;
  font-family: "Roboto";
  font-size: 24px;
  line-height: 28px;
  color: #ffffff;
  text-transform: capitalize;
}
.todos-wrapper {
  display: flex;
  flex-direction: column;
  width: 700px;
  margin: 0 auto;
  margin-top: 30px;
  background: #ffffff;
  border-radius: 5px;
}
.todo-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 46px;
  margin: 17px 25px;
  background: #ffffff;
}
.todo-item.delition {
  animation: opacity 1s ease-in-out;
}
.todo-date {
  height: 46px;
  font-size: 14px;
  line-height: 46px;
  font-family: "Roboto";
  background: #ffffff;
  border-bottom: 1px solid #868686;
}
.cerf {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 490px;
  height: 46px;
  border-bottom: 1px solid #868686;
}

.description {
  font-family: "Roboto";
  font-size: 16px;
  line-height: 20px;
  color: rgba(0, 0, 0, 0.82);
  cursor: pointer;
  height: 20px;
  overflow: auto;
}
.todo__text_isShow {
  text-decoration: line-through;
}

.wraper-btn {
  display: flex;
  margin-left: 7px;
}

.btn-complete {
  margin-bottom: 9px;
  margin-right: 15px;
  width: 36px;
  height: 36px;
  border-radius: 5px;
  background: #62abd9;
  border-radius: 5px;
}

.btn-delete {
  background: #62abd9;
  border-radius: 5px;
  margin-bottom: 9px;
  width: 36px;
  height: 36px;
  border-radius: 5px;
  border-radius: 5px;
}
.btn-check {
  display: none;
  background: #62abd9;
  border-radius: 5px;
  margin-bottom: 9px;
  width: 36px;
  height: 36px;
  border-radius: 5px;
  border-radius: 5px;
}
img {
  width: 20px;
  height: 20px;
}
</style>
