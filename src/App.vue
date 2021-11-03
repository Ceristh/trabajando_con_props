<template>
  <div id="app" class="container">
    <img alt="Vue logo" src="@/assets/logo.png"/>
    <h1 class="my-3">Trabajando con Props</h1>
    <form v-on:submit.prevent="agregarTarea" class="form-group row mb-5">
      <label for="tarea" class="col mb-2 mr-2 col-form-label text-right"><h5>Tarea:</h5></label>
      <input type="text" id="tarea" v-model="nuevaTarea" placeholder="Ingrese nueva tarea" class="col mb-2 mr-3 col-form-label"/>
      <button @click="agregarTarea" class="btn btn-info col mb-2 mr-3 col-form-label">Crear</button>
    </form>
    <TodoList v-bind:tasks="tasks" @remueve="eliminar"/>
    <h2 class="my-5">{{errorMessage}}</h2>
  </div>
</template>

<script>
import TodoList from "@/components/TodoList";
export default {
  name: "App",
  data() {
    return {
      nuevaTarea: "",
      tasks: [],
      errorMessage: "",
    };
  },
  components: {
    TodoList,
  },
  methods: {
    agregarTarea() {
      if (this.nuevaTarea == "") return false
      
      // Comprueba si la tarea es similar, estando en mayusculas a minusculas.
      // Me ayude con vuejs.org
      let similarTareas = this.tasks.map((task) =>
          task.toLowerCase().replace(" ", "")
      );
      if (!similarTareas.includes(this.nuevaTarea.toLowerCase().replace(" ", ""))) {
        this.tasks.push(this.nuevaTarea);
        this.errorMessage = "";
      } else {
        this.errorMessage = "La tarea, ya esta!!";
      }
      this.nuevaTarea = "";
    },
    eliminar(index){
      this.tasks.splice(index,1);
    }
  },
};
</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 50px;
  },
  h2 {
    height: 25px;
    width: 100%;
  }
</style>