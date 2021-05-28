<template>
  <form action="" class="form" @submit.prevent="submitTask">
    <div class="form-group input">
      <input
        type="text"
        autocomplete="off"
        placeholder="Add details"
        v-model="task"
      />
    </div>
    <div class="form-group">
      <button type="submit">Add</button>
    </div>
  </form>
</template>

<script>
import { ref } from "vue";
export default {
  name: "PxFormTask",

  setup(props) {
    let task = ref("");
    let message = ref("");
    const submitTask = async () => {
      if (task.value != "") {
        try {
          const API = "https://api-fake-todo-app-2021.herokuapp.com/task";
          const config = {
            method: "POST",
            body: JSON.stringify({
              task: task.value,
              status: false,
            }),
            headers: {
              "Content-type": "application/json; charset=UTF-8",
            },
          };

          const response = await fetch(API, config);

          // Validate status code
          if (!response.ok) {
            if (response.status == 404) {
              message.value = "Error de conexion con el servicio";
              console.error(message.value);
            }
          }
          console.log(response.status);
          const data = await response.json();
          task.value = "";
          console.log(data);
        } catch (error) {
          console.error(error);
        }
      } else {
        message.value = "Ingrese una tarea, porfavor";
        console.error(message.value);
      }
    };

    return {
      submitTask,
      task,
    };
  },
};
</script>

<style lang="scss" scoped>
@import "~@/assets/sass/components/_PxFormTask.scss";
</style>
