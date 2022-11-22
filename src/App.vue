<template>
  <div class="app">
    <div class="todos">
      <Todos :title="'Today'" />
    </div>
  </div>
</template>

<script>
import Todos from "./components/Todos/Todos.vue";

export default {
  components: {
    Todos,
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Inter:wght@400;700&display=swap");

*,
::after,
::before {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background: #171930;

  font-family: "Inter", sans-serif;
  color: #fff;

  padding: 0 16px;
}

.todos {
  display: flex;
  justify-content: center;
  margin-top: 40px;

  @media (max-width: 600px) {
    margin-top: 16px;
  }
}
</style>
