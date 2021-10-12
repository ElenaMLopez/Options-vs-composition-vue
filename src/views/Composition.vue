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
import { ref, computed, watch } from 'vue';
//TODO: Add reactive objects instead ref method

export default {
  setup () {
    let newTodoName = ref('');
    let todos = ref([],);
 
    const swearwords = ['fart', 'whore', 'ass', 'butt' ];

    let todosCount = computed(() => {
      return todos.value.length
    })

    function addTodo() {
      let newTodo = {
        id: Date.now(),
        name: newTodoName.value
      }
      todos.value.push(newTodo);
      newTodoName.value = '';
    }
    function deleteTodo(index) {
      todos.value.splice(index, 1);
    }

    watch(newTodoName, (newValue) => {
      if(swearwords.includes(newValue.toLowerCase())) {
        newTodoName.value = ''
        alert(`You must NEVER say ${newValue}!!`)
      }
    })


    return {
      newTodoName,
      todos,
      addTodo,
      deleteTodo,
      todosCount
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