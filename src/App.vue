<template>
  <div id="aplicacion">
    <h1>TODO LIST</h1>
    <small>by <a href="https://academia.programee.com">programee</a></small>
    <div class="contenido">
      <!-- Formulario para agregar una nueva tarea -->
      <div class="add-todo">
        <!-- Campo de entrada para la nueva tarea -->
        <input v-model="newTodo" @keyup.enter="addTodo" type="text" placeholder="Añadir una nueva tarea" />
        <!-- Botón para agregar la tarea -->
        <button @click="addTodo">Añadir</button>
      </div>
      <!-- Lista de tareas -->
      <ul>
        <!-- Renderizar las tareas con v-for -->
        <li v-for="todo in todos" :key="todo.id" :class="{ completed: todo.completed }">
          <!-- Texto de la tarea -->
          <span @click="toggleComplete(todo.id)">{{ todo.text }}</span>
          <!-- Botón para completar la tarea -->
          <button class="green" @click="toggleComplete(todo.id)">Completar</button>
          <!-- Botón para eliminar la tarea -->
          <button @click="deleteTodo(todo.id)">Eliminar</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
// Importar la función ref desde Vue
import { ref } from 'vue';

// Definir una lista de tareas inicial
const todos = ref([
  { id: 1, text: 'Aprender Vue.js', completed: false },
  { id: 2, text: 'Dejar una reseña en el curso', completed: false },
  { id: 3, text: 'Terminar este primer proyecto', completed: false },
]);

// Definir un valor reactivo para la nueva tarea
const newTodo = ref('');

// Función para agregar una nueva tarea
const addTodo = () => {
  if (newTodo.value.trim() !== '') {
    todos.value.push({
      id: Date.now(),
      text: newTodo.value,
      completed: false
    });
    newTodo.value = '';
  }
};

// Función para marcar una tarea como completada o no completada
const toggleComplete = (id) => {
  const todo = todos.value.find(todo => todo.id === id);
  if (todo) {
    todo.completed = !todo.completed;
  }
};

// Función para eliminar una tarea de la lista
const deleteTodo = (id) => {
  todos.value = todos.value.filter(todo => todo.id !== id);
};
</script>

<style>
#aplicacion {
  font-family: Arial, sans-serif;
  text-align: center;
  margin-top: 50px;
  width: 100%;
}

.add-todo {
  margin-bottom: 20px;
}

.add-todo input {
  padding: 10px;
  font-size: 16px;
  width: 200px;
  margin-right: 10px;
}

.add-todo button {
  padding: 10px;
  font-size: 16px;
}

.contenido {
  display: flex;
  width: 100%;
  flex-direction: column;
  margin-top: 20px;
  gap: 30px;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px;
  font-size: 18px;
  border-bottom: 1px solid #ccc;
}

li.completed span {
  text-decoration: line-through;
  color: gray;
}

li button {
  background: none;
  border: none;
  color: red;
  cursor: pointer;
}

li button.green {
  color: aquamarine;
}
</style>
