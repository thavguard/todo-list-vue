<template>
  <div class="todos">
    <div class="title">{{ title }}</div>
    <Todo
      v-for="todo in todos"
      :id="todo.id"
      :title="todo.title"
      :isDone="todo.isDone"
      :key="todo.id"
      @setDone="(isDone) => (todo.isDone = !isDone)"
    />
    <div class="create-todo">
      <input type="text" placeholder="Add todo..." @keydown="addTodo" />
    </div>
  </div>
</template>

<script>
import Todo from "../Todo/Todo.vue";

export default {
  props: {
    title: String,
  },
  data() {
    return {
      todos: [
        { id: 0, isDone: false, title: "Todo" },
        { id: 0, isDone: false, title: "Todo" },
        { id: 0, isDone: false, title: "Todo" },
        { id: 0, isDone: false, title: "Todo" },
      ],
    };
  },
  components: {
    Todo,
  },
  methods: {
    addTodo(e) {
      if (e.key === "Enter") {
        this.todos.push({});
      }
    },
  },
};
</script>

<style scoped lang="scss">
.todos {
  margin-bottom: 36px;
}
.title {
  font-size: 18px;

  margin-bottom: 16px;
}

.create-todo {
  input {
    display: flex;
    align-items: center;
    padding: 20px;
    border: none;

    color: #fff;
    font-size: 16px;
    font-family: "Inter", sans-serif;

    background: #1e203b;
    border-radius: 11px;

    box-shadow: rgba(0, 0, 0, 0.1) 0px 4px 12px;

    cursor: pointer;

    &::placeholder {
      font-family: "Inter", sans-serif;
    }

    &:focus {
      outline: none;
    }
  }
}
</style>
