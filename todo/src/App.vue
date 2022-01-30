<template>
  <h1>ToDo App</h1>
  <form @submit.prevent="addContents()">
    <label>New ToDo </label>
    <input type="text" v-model="content" />
    <button>Add ToDo</button>
  </form>

  <h2>ToDo List {{ todos.length }}</h2>
  <ul>
    <li v-for="(todo, index) in todos" :key-"index">
      <span :class="{ done: todo.done, notDone: !todo.done }" @click="doContent(todo)"> {{ todo.content }} </span>
      <button @click="removeContents(index)">X</button>
    </li>
  </ul>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "App",
  data() {
    return {
      todos: [],
      content: "",
    };
  },
  methods: {
    addContents() {
      this.debug(this.content);
      if (this.content.length < 1) return; // if length < 1 will not add to list
      this.todos.push({
        // push to 'todos' list
        content: this.content,
        done: false,
      });
      this.content = ""; // clear content value
    },
    removeContents(i) {
      this.todos.splice(i, 1);
      this.debug(`remove todos at -> ${i}`);
    },
    doContent(content) {
      content.done = !content.done;
      this.debug(`do content ${JSON.stringify(content)}`);
    },
    debug(vars) {
      console.log(`dubug: ${vars}`);
    },
  },
};
</script>

<style>
  .done {
    opacity: 0.3;
    text-decoration: line-through;
  }
  .notDone {
    color: rgb(255, 189, 23);
    text-decoration: underline;
  }
</style>
