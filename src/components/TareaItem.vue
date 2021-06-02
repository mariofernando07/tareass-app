<template>
  <div
    class="alert alert-warning d-flex justify-content-between align-items-center"
  >
    <p class="m-0" :style="{'text-decoration': tarea.estado ? 'line-through' : 'none'}">
      {{ tarea.texto }}
    </p>
    <div>
      <i
        class="fas mx-2 text-success"
        :class="tarea.estado ? 'fa-undo-alt' :'fa-check-circle'"
        role="button"
        @click="update"
      ></i>
      <i
        class="fas fa-minus-circle text-danger"
        role="button"
        @click="eliminar"
      ></i>
    </div>
  </div>
</template>

<script>
import { inject } from "vue";
export default {
  props: {
    tarea: {
      type: Object,
    },
  },
  setup(props) {
    const tareas = inject("tareas");

    const eliminar = () => {
      tareas.value = tareas.value.filter(
        (tarea) => tarea.id !== props.tarea.id
      );
    };

    const update = () => {
      props.tarea.estado = !props.tarea.estado;
    };

    return {
      update,
      eliminar,
    };
  },
};
</script>

<style>
</style>