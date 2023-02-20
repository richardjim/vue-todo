<script setup>
import Create from '../components/Create.vue';
import { ref } from 'vue';
import { uid } from 'uid';
import { Icon } from '@iconify/vue'

const todoList = ref([])
const createTodo = (todo) => {
  todoList.value.push(
    {
      id: uid(),
      todo,
      isCompleted: null,
      isEditing: null
    }
  );

};

const toggleEditTodo = (index) => {
  todoList.value[index].isEditing = !todoList.value[index].isEditing;
};
</script>

<template>
  <main>
    <h1> Create Todo</h1>
    <Create @create-todo="createTodo" />
    <ul class="todo-list">
      <li v-for="todo in todoList" :key="todo.id">
        <div class="todo">
          <input type="checkbox" v-if="todo.isEditing" :value="todo.todo" @edit-todo="toggleEditTodo">
          <span>{{ todo.todo }}</span>
        </div>
        <div class="todo-actions">
          <Icon icon="ph:check-circle" class="icon" color="#41b080" />
          <Icon icon="ph:pencil-fill" @click="$emit('edit-todo', index)" class="icon" color="#41b080" />
          <Icon icon="ph:trash-fill" class="icon" color="#f95e5e" />
        </div>
      </li>
    </ul>
  </main>
</template>

<style scoped lang="scss">
main {
  display: flex;
  flex-direction: column;
  max-width: 500px;
  width: 100%;
  margin: 0 auto;
  padding: 40px 16px;
}

li {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 16px 10px;
  background-color: #f1f1f1;
  box-shadow: 0 20px 25px -5px rgb(0 0 0 / 0.1),
    0 8px 10px -6px rgb(0 0 0 / 0.1);

  &:hover {
    .todo-actions {
      opacity: 1;
    }
  }
}

h1 {
  margin-bottom: 16px;
  text-align: center;
}

.todo-list {
  display: flex;
  flex-direction: column;
  list-style: none;
  margin-top: 24px;
  gap: 20px;
}

.todos-msg {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  margin-top: 24px;
}

.todo {
  flex: 1;

  input[type="text"] {
    width: 100%;
    padding: 2px 6px;
    border: 2px solid #41b080;
  }
}

.todo-actions {
  display: flex;
  gap: 6px;
  opacity: 0;
  transition: 150ms ease-in-out;

  .icon {
    cursor: pointer;
  }
}
</style>
