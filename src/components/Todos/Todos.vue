<template>
  <div class="container">
    <div v-if="todos.length">
      <div class="header">
        <div class="title">{{ title }}</div>
        <div class="filter">
          <button
            :class="`${todosType === 'all' && 'active'} filter__item`"
            @click="todosType = 'all'"
          >
            all
          </button>
          <button
            :class="`${todosType === 'completed' && 'active'} filter__item`"
            @click="todosType = 'completed'"
          >
            completed
          </button>
          <button
            :class="`${todosType === 'notCompleted' && 'active'} filter__item`"
            @click="todosType = 'notCompleted'"
          >
            not completed
          </button>
        </div>
      </div>
      <transition-group name="list" tag="div">
        <Todo
          v-for="(todo, index) in todos.filter(filterTodos)"
          :id="todo.id"
          :title="todo.title"
          :isDone="todo.isDone"
          :key="todo.id"
          @setDone="(isDone) => (todo.isDone = !isDone)"
          @deleteTodo="() => deleteTodo(index)"
        />
      </transition-group>
    </div>
    <div v-else class="nothing">You have nothing to do yet 📝</div>
    <div class="create-todo">
      <input
        type="text"
        placeholder="Add todo..."
        v-model="todo"
        @keydown="addTodo"
      />
    </div>
  </div>
</template>

<script>
import Todo from "../Todo/Todo.vue";
import JSConfetti from "js-confetti";

export default {
  props: {
    title: String,
  },
  data() {
    return {
      todos: JSON.parse(localStorage.getItem("todos")) || [],
      todo: "",
      nextTodoId: 0,
      todosType: "all", // all, completed, notCompleted
    };
  },
  components: {
    Todo,
  },
  methods: {
    addTodo(e) {
      if (e.key === "Enter" && this.todo) {
        this.todos.push({
          id: this.nextTodoId++,
          isDone: this.todosType === "completed",
          title: this.todo,
          createdAt: Date.now(),
        });
        this.todo = "";
      }
    },
    deleteTodo(index) {
      console.log(index);
      this.todos.splice(index, 1);
    },
    filterTodos(todo) {
      switch (this.todosType) {
        case "completed":
          return todo.isDone;

        case "notCompleted":
          return !todo.isDone;

        default:
          return true;
      }
    },
  },
  watch: {
    todos: {
      handler(newTodos) {
        localStorage.setItem("todos", JSON.stringify(newTodos));

        const isAllDone = newTodos.filter((item) => !item.isDone);

        if (!isAllDone.length) {
          const jsConfetti = new JSConfetti();
          jsConfetti.addConfetti();
        }
      },
      deep: true,
    },
  },
  mounted() {},
};
</script>

<style scoped lang="scss">
.container {
  max-width: 100%;

  margin-bottom: 36px;
  margin-right: 16px;
}

.list {
  &-enter-active,
  &-leave-active,
  &-move {
    transition: all 0.4s;
  }
  &-enter, &-leave-to /* &-leave-active до версии 2.1.8 */ {
    opacity: 10%;
    transform: translateX(100%);
  }
}

.header {
  display: flex;
  align-items: center;
  margin-bottom: 16px;
}

.filter {
  display: flex;
  align-items: center;

  &__item {
    background: coral;

    padding: 4px 8px;

    margin-right: 8px;

    border-radius: 4px;

    cursor: pointer;

    user-select: none;

    font-family: inherit;
    color: #fff;
    font-size: 16px;

    &:active {
      transform: scale(0.99);
    }
  }
}
.active {
  background: darkorchid;
}

.title {
  font-size: 24px;

  margin-right: 16px;
}

.nothing {
  font-size: 22px;

  margin-bottom: 16px;
}

.create-todo {
  input {
    display: flex;
    align-items: center;
    padding: 20px;
    border: none;
    width: 100%;

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
