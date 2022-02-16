<template>
  <div>
    <div class="todos-wrapper">
      <div v-for="(todo, i) in todos" :key="i" class="todo-item">
        <div class="todo-date">{{ todo.dates }}</div>
        <div class="cerf">
          <div
            class="description"
            :class="{ todo__text_isShow: todo.isComplete }"
          >
            {{ todo.text }}
          </div>
          <div class="wraper-btn">
            <button class="btn-complete" v-on:click="$emit('btn-complete', i)">
              P
            </button>
            <button class="btn-delete" v-on:click="$emit('remove-todo', i)">
              X
            </button>
            <button class="btn-check" v-on:click="$emit('btn-check', i)">
              V
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    todos: {
      type: [Object, Array],
      required: true,
    },
  },
};
</script>