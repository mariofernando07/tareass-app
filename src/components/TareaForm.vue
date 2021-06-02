<template>
  <form @submit.prevent="agregarTarea">
    <input
      type="text"
      class="form-control my-2"
      placeholder="Ingrese una tarea"
      v-model.trim="texto"
    />
    <button class="btn btn-primary w-100">Agregar</button>
  </form>
</template>

<script>
import { inject, ref } from "vue";
export default {
  setup() {
    const texto = ref("");
    const tareas = inject("tareas");

    const agregarTarea = () => {
      if (texto.value === "") {
        return console.log("texto vacio");
      }

      const tarea = {
        id: Date.now(),
        texto: texto.value,
        estado: false,
      };
      tareas.value.push(tarea)
    };
    return {
      agregarTarea,
      texto,
    };
  },
};
</script>

<style>
</style>