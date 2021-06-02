<template>
  <h1>App Tareas</h1>
  <tarea-form />
  <tarea-item
    class="mt-2"
    v-for="tarea in tareas"
    :key="tarea.id"
    :tarea="tarea"
  />

  <div class="alert alert-dark mt-3" v-if="!tareas.length">
    Sin tareas pendientes 😍
  </div>
</template>

<script>
import { provide, ref, watchEffect } from "vue";
import TareaForm from "@/components/TareaForm";
import TareaItem from "@/components/TareaItem";
export default {
  components: {
    TareaForm,
    TareaItem,
  },
  setup() {
    const tareas = ref([]);
    provide("tareas", tareas);

    if (localStorage.getItem("tareas")) {
      tareas.value = JSON.parse(localStorage.getItem("tareas"));
    }

    watchEffect(() => {
      localStorage.setItem("tareas", JSON.stringify(tareas.value));
    });

    return {
      tareas,
    };
  },
};
</script>

<style>
</style>