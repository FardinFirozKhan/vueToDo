<template>
  <div :class="['todo-app', isDarkMode ? 'bg-dark text-light' : 'bg-light text-dark']">
    <div class="text-end mb-3">
      <button 
        class="btn btn-sm" 
        :class="isDarkMode ? 'btn-light' : 'btn-dark'" 
        @click="toggleDarkMode"
      >
        {{ isDarkMode ? 'Light Mode' : 'Dark Mode' }}
      </button>
    </div>

   
    <h1 class="text-center mb-4">My Todo List</h1>

  
    <div class="input-group mb-4">
      <input 
        type="text" 
        class="form-control form-control-lg" 
        placeholder="Add a new todo" 
        v-model="newTodo" 
        @keyup.enter="addTodo"
        :class="isDarkMode ? 'bg-secondary text-light' : ''"
      />
      <button class="btn btn-primary btn-lg" @click="addTodo">Add</button>
    </div>

    
    <ul class="list-group">
      <li 
        v-for="(todo, index) in todos" 
        :key="index" 
        :class="['list-group-item', 'd-flex', 'justify-content-between', 'align-items-center', isDarkMode ? 'bg-dark text-light border-secondary' : '', todo.completed ? 'bg-success text-white' : '']"
      >
        <div class="d-flex align-items-center">
          <input 
            type="checkbox" 
            class="form-check-input me-3" 
            v-model="todo.completed" 
          />
         
          <span 
            v-if="!todo.isEditing" 
            :class="['todo-text', todo.completed ? 'text-decoration-line-through' : '']">
            {{ todo.text }}
          </span>
          <input 
            v-else 
            type="text" 
            class="form-control form-control-sm d-inline-block w-75" 
            v-model="todo.text" 
            @keyup.enter="saveTodo(todo)"
          />
        </div>
        <div>
          <button 
            class="btn btn-warning btn-sm me-2" 
            v-if="!todo.isEditing" 
            @click="editTodo(todo)">
            Edit
          </button>
          <button 
            class="btn btn-success btn-sm me-2" 
            v-if="todo.isEditing" 
            @click="saveTodo(todo)">
            Save
          </button>
          <button 
            class="btn btn-danger btn-sm" 
            @click="deleteTodo(index)">Delete
          </button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodo: '',
      todos: [],
      isDarkMode: false
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() !== '') {
        this.todos.push({ text: this.newTodo, completed: false, isEditing: false });
        this.newTodo = '';
      }
    },
    deleteTodo(index) {
      this.todos.splice(index, 1);
    },
    editTodo(todo) {
      todo.isEditing = true;
    },
    saveTodo(todo) {
      todo.isEditing = false;
    },
    toggleDarkMode() {
      this.isDarkMode = !this.isDarkMode;
    }
  }
}
</script>

<style scoped>

.todo-app {
  max-width: 600px;
  margin: 50px auto;
  border-radius: 10px;
  padding: 20px;
  transition: background-color 0.5s, color 0.5s;
}


.bg-dark {
  background-color: #343a40 !important;
}

.bg-light {
  background-color: #f8f9fa !important;
}

.text-light {
  color: #f8f9fa !important;
}

.text-dark {
  color: #343a40 !important;
}


button {
  transition: background-color 0.3s, color 0.3s;
}

button:hover {
  transform: translateY(-2px);
}

.border-secondary {
  border-color: #6c757d !important;
}


.bg-secondary {
  background-color: #6c757d !important;
}


.form-check-input {
  width: 1.5rem;
  height: 1.5rem;
  cursor: pointer;
}

.btn-primary {
  background-color: #007bff;
}

.btn-primary:hover {
  background-color: #0056b3;
}

.btn-warning {
  background-color: #f0ad4e;
}

.btn-warning:hover {
  background-color: #ec971f;
}

.btn-danger {
  background-color: #d9534f;
}

.btn-danger:hover {
  background-color: #c9302c;
}

.text-decoration-line-through {
  text-decoration: line-through;
}

.list-group-item {
  padding: 15px;
  border-radius: 0.25rem;
  transition: background-color 0.3s, color 0.3s;
}
</style>
