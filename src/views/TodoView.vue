<template>
    <div>
        <div class="todo">
            Voici ma super ToDo List
        </div>
        <h4 v-if="IsInvalid">RENSEIGNE LES CHAMPS</h4>
        <form @submit.prevent="AddTodo()">
            <label for="input_text">Nom
                <input class="input_todo" v-model="name" type="text" id="heure" name="input_text">
            </label>
           <label style="margin-left:20px;" for="input_heure">Nombre d'heures
                <input class="input_todo" v-model="hours" type="number" id="heure"
                       name="input_heure" min="1">
           </label>
           <select class="input_todo" style="margin-left:20px;" v-model="users" name="users">
               <option value="Kévin">Théo</option>
               <option value="Kévin">Kévin</option>
               <option value="Kévin">Quentin</option>
           </select>
           <button class="input_todo" style="margin-left:20px;" type="submit" value="submit">
               Ajouter
           </button>
        </form>
        <div class="index_todo" v-for="todo in todos" v-bind:key="todo.name">
          <div class="col">{{ todo.name }}</div>
          <div class="col">{{ todo.hours }}</div>
          <div class="col">{{ todo.users }}</div>
          <div class="col">
            <button @click="todos.splice(index, 1)">
                Delete
            </button>
          </div>
        </div>
        <div v-if="todos.length > 0">
            <button @click="todos = []">
                Delete ALL
            </button>
        </div>
    </div>
</template>

<script>
export default {
  name: 'TodoComponent',
  data() {
    return {
      todos: [],
      name: '',
      hours: '',
      users: '',
      IsInvalid: false,
    };
  },
  methods: {
    AddTodo() {
      if (this.IsVerified()) {
        this.todos.push({
          name: this.name,
          hours: this.hours,
          users: this.users,
        });
      }
    },
    IsVerified() {
      if (this.name === '' || this.hours === '' || this.users === '') {
        this.IsInvalid = true;
        return false;
      }
      this.IsInvalid = false;
      return true;
    },
  },
};
</script>

<style scoped>
  .todo{
    font-size: 22px;
    margin-bottom: 20px;
  }

  .index_todo {
      display: flex;
      justify-content: space-around;
      border: solid black 1px;
      margin-top: 40px;
      width: 80%;
      border-radius: 10px;
      margin-right: auto;
      margin-left: auto;
      padding: 20px;
  }

  .input_todo {
      padding: 8px;
      border-radius: 5px;
  }

</style>
