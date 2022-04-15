<template>
    <div>
        <div class="todo">
            Voici votre super ToDo List
        </div>
        <h4>Vous avez {{todos.length}} Todos</h4>
        <h4 v-if="IsInvalid">Veuillez rensergner tous les champs</h4>
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
            <button class="button_delete" @click="todos.splice(index, 1)">
                <i class="fa fa-trash-o" aria-hidden="true"></i>
            </button>
            <button class="button_edit">
                <i class="fa fa-pencil" aria-hidden="true"></i>
            </button>
          </div>
        </div>
        <div v-if="todos.length > 0">
            <button  style="margin-top:20px;" @click="todos = []">
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
          status: 'A venir',
        });
        this.name = '';
        this.hours = '';
        this.users = '';
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
      width: 90%;
      border-radius: 10px;
      margin-right: auto;
      margin-left: auto;
      padding: 20px;
  }

  .input_todo {
      padding: 8px;
      border-radius: 5px;
  }

  .button_delete {
    color: white;
    background-color: red;
    padding: 10px;
    border: none;
    font-size: 15px;
    border-radius: 50%;
    margin-right: 15px;
  }

  .button_edit {
    color: white;
    background-color: blue;
    padding: 10px;
    border: none;
    font-size: 15px;
    border-radius: 50%;
  }

</style>
