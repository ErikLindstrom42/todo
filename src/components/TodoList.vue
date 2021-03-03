<template>
  <div>
    <h3>ToDo List</h3>
    <h5>There are {{ itemsRemainingMessage }} items left to do today</h5>
    <div v-for="item in todos" :key="item.id">
      <todo-item :todo="item" @status-change="handleStatusChange" />
    </div>
  </div>
</template>
<script>
import { todoItems } from "../data";
import TodoItem from "./TodoItem.vue";

export default {
  components: { TodoItem },
  methods: {
    handleStatusChange(item) {
      item.complete = !item.complete;
      console.log(item);
    },
  },
  data() {
    return {
      todos: [...todoItems],
    };
  },
  computed: {
    itemsRemainingMessage() {
      const remaining = this.todos.filter((t) => !t.complete).length;
      if (remaining == 1) {
        return "There is 1 item left to do today";
      }
      return `There are ${remaining} items left to do today`;
    },
  },
};
</script>

<style scoped>
.card {
  background: black;
}
</style>