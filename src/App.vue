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

<style>
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
}


.todos {
  display: flex;
  justify-content: center;
  margin-top: 40px;
}
</style>
