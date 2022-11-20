<template>
  <div class="todo">
    <div class="flex" @click="setCheckbox">
      <div class="checkbox" :data-checked="isDone"></div>
      <div class="title" :data-checked="isDone">{{ title }}</div>
    </div>
    <div class="remove" @click="deleteTodo">❌</div>
  </div>
</template>

<script>
export default {
  props: {
    id: Number,
    title: String,
    isDone: Boolean,
  },
  emits: {
    setDone: null,
    deleteTodo: null,
  },
  methods: {
    setCheckbox() {
      this.$emit("setDone", this.isDone);
    },
    deleteTodo() {
      this.$emit("deleteTodo", this.id);
    },
  },
};
</script>

<style scoped lang="scss">
.todo {
  display: flex;
  justify-content: space-between;
  align-items: center;

  padding: 20px;

  max-width: 600px;

  background: #1e203b;
  border-radius: 11px;

  box-shadow: rgba(0, 0, 0, 0.1) 0px 4px 12px;

  transition: all 0.1s ease-in-out;

  cursor: pointer;

  &:hover {
    transform: scale(1.05);
  }

  margin-bottom: 16px;
}

.checkbox {
  width: 20px;
  height: 20px;

  border: solid 1.3px #f18c27;

  border-radius: 50%;

  margin-right: 16px;

  &[data-checked="true"] {
    background: #f18c27;
    box-shadow: 0px 0px 0px 1.3px rgba(255, 255, 255, 1) inset;
  }
}

.title {
  font-family: "Inter", sans-serif;
  font-style: normal;
  font-weight: 400;
  font-size: 16px;
  line-height: 25px;

  margin-right: 16px;

  max-width: 460px;
  word-wrap: break-word;

  &[data-checked="true"] {
    text-decoration: line-through;

    color: #eee;
  }
}

.flex {
  display: flex;
  align-items: center;
  flex: 1;
  // padding: 20px 0 20px;
}

.remove {
  // padding: 20px;

  user-select: none;
}
</style>
