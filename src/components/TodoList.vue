<template>
  <div class="hijo">
    <table class="table table-borderless">
      <tbody>
        <tr v-for="(task, index) in tasks" :key=task>
          <td>{{index+1}}</td>
          <td>{{task}}</td>
          <td><button @click="eliminar(index)" class="btn btn-block btn-success">Eliminar</button></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
  export default {
    name: 'TodoList',
    props: {
      tasks: Array,
    },
    methods: {
      eliminar(index) {
        this.$emit("remueve",index);
      }
    }
  }
</script>