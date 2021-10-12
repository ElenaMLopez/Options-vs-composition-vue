<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <h3>You have {{ todosCount }} Todos!</h3>
    <input
      v-model="newTodoName"
      @keyup.enter="addTodo"
      type="text" 
      placeholder="Add a todo"
    >
  </div>
  <div>
    <ul>
      <li v-for="(todo, index) in todos" :key="todo.id">
        <span>{{ todo.name }}</span>
        <button @click="deleteTodo(index)">
          X
        </button>
      </li>
    </ul>
  </div>
</template>

<script>

export default {
  data() {
    return {
      newTodoName: '',
      todos: [ 
        {
          id: 1,
          name: 'One'
        },
        {
          id: 2,
          name: 'Two'
        },
        {
          id: 3,
          name: 'Three'
        },
      ],
      swearwords: ['fart', 'whore', 'ass', 'butt' ]
    }
  },
  computed: {
    todosCount() {
      return this.todos.length;
    }

  },
  methods: {
    addTodo() {
      let newTodo = {
        id: Date.now(),
        name: this.newTodoName
      }
      this.todos.push(newTodo);
      this.newTodoName = ''
    },
    deleteTodo(index) {
      this.todos.splice(index, 1);
    }
  },
  watch: {
    newTodoName(newValue) {
      if(this.swearwords.includes(newValue.toLowerCase())) {
        this.newTodoName = ''
        alert(`You must NEVER say ${newValue}`)
      }

    }
  }
}
</script>
<style scoped>
ul {
  list-style-type: none;
  margin: 20px auto 0;
  padding: 0;
  width: 200px;
}
li {
  border: 1px solid #456a45;
  display: flex;
  margin-bottom: 10px;
}
li span {
  flex: 1;
}
</style>
