<template>
  <div class="detele__all" v-if="dataTask.length > 0">
    <button class="detele__all-btn" @click="handleDeleteAllTask()">
      <font-awesome-icon icon="trash-alt" />
      delete all
    </button>
  </div>
</template>

<script>
import { ref, inject } from "vue";

import { library } from "@fortawesome/fontawesome-svg-core";
import { faTrashAlt } from "@fortawesome/free-solid-svg-icons";
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
library.add(faTrashAlt);

export default {
  name: "PxBtnDeleteCompletedTask",
  components: {
    FontAwesomeIcon,
  },
  setup() {
    const dataTask = inject("dataTodoListState");
    let message = ref("");

    const handleDeleteAllTask = async () => {
      dataTask.value.forEach(async (task) => {
        console.log(`Se eliminaron todas las tareas ${task.id}`);
        try {
          const API = "https://api-fake-todo-app-2021.herokuapp.com/task";

          const config = {
            method: "DELETE",
            body: JSON.stringify({
              id: task.id,
              task: task.task,
              status: task.status,
            }),
            headers: {
              "Content-type": "application/json; charset=UTF-8",
            },
          };

          const response = await fetch(`${API}/${task.id}`, config);

          // Validate status code
          if (!response.ok) {
            if (response.status == 404) {
              message.value = "Error de conexion con el servicio";
              console.error(message.value);
            }
          }
          const data = await response.json();
        } catch (error) {
          console.log(error);
        }
      });
      const newTaskListDeleteAll = dataTask.value.filter((task) => {
        return task.status != true;
      });
      dataTask.value = newTaskListDeleteAll;
    };

    return {
      handleDeleteAllTask,
      dataTask,
    };
  },
};
</script>

<style lang="scss" scoped>
.detele__all {
  width: 100%;
  text-align: right;
  margin: 32px 0 0 0;
  &-btn {
    width: 124px;
    height: 40px;
    border-radius: 4px;
    background: #eb5757;
    color: #ffffff;
    border: 1px solid #eb5757;
    margin: 0;
    padding: 0;
    font-size: 12px;
    font-family: "Montserrat-Medium";
    transition: 0.4s ease all;
    svg {
      margin: 0 5.5px 0 0;
      font-size: 12px;
    }
    &:hover {
      background: #ffffff;
      color: #eb5757;
    }
  }
}
</style>
