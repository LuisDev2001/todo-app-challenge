<template>
  <div class="task">
    <div class="checkbox">
      <input type="hidden" :value="idTask" class="task-id" />
      <input
        type="checkbox"
        v-model="checkBoxState"
        @change="handleUpdateTask"
      />
      <label>
        <font-awesome-icon icon="check" />
      </label>
    </div>
    <span
      :class="{
        'result-todo__text': true,
        'is-checked': checkBoxState,
      }"
      v-text="taskText"
    >
    </span>
  </div>
  <div
    v-if="path == '/completed-task'"
    @click="handleDeleteTask"
    class="result-todo__delete"
  >
    <font-awesome-icon icon="trash-alt" />
  </div>
</template>

<script>
import { ref, inject } from "vue";
import { useRoute } from "vue-router";

import { library } from "@fortawesome/fontawesome-svg-core";
import { faCheck, faTrashAlt } from "@fortawesome/free-solid-svg-icons";
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";

library.add(faCheck), faTrashAlt;

export default {
  name: "PxTask",
  components: {
    FontAwesomeIcon,
  },
  props: {
    taskText: String,
    checkBoxState: Boolean,
    idTask: Number,
  },
  setup(props) {
    const path = useRoute().path;
    const dataTask = inject("dataTodoListState");
    let message = ref("");

    // Method for update task
    const handleUpdateTask = async () => {
      try {
        const API = "https://api-fake-todo-app-2021.herokuapp.com/task";

        const config = {
          method: "PUT",
          body: JSON.stringify({
            id: props.idTask,
            task: props.taskText,
            status: props.checkBoxState,
          }),
          headers: {
            "Content-type": "application/json; charset=UTF-8",
          },
        };

        const response = await fetch(`${API}/${props.idTask}`, config);

        // Validate status code
        if (!response.ok) {
          if (response.status == 404) {
            message.value = "Error de conexion con el servicio";
            console.error(message.value);
          }
        }
        const data = await response.json();
        console.log(`Se actualizo la tarea con el id ${props.idTask}`);
      } catch (error) {
        console.log(error);
      }
    };

    //Method for delete task
    const handleDeleteTask = async () => {
      try {
        const API = "https://api-fake-todo-app-2021.herokuapp.com/task";

        const config = {
          method: "DELETE",
          body: JSON.stringify({
            id: props.idTask,
            task: props.taskText,
            status: props.checkBoxState,
          }),
          headers: {
            "Content-type": "application/json; charset=UTF-8",
          },
        };

        const response = await fetch(`${API}/${props.idTask}`, config);

        // Validate status code
        if (!response.ok) {
          if (response.status == 404) {
            message.value = "Error de conexion con el servicio";
            console.error(message.value);
          }
        }
        const data = await response.json();
        console.log(`Se eliminó la tarea con el id ${props.idTask}`);

        const newTaskListCompleted = dataTask.value.filter((task) => {
          return task.id !== props.idTask;
        });
        dataTask.value = newTaskListCompleted;
      } catch (error) {
        console.log(error);
      }
    };

    return {
      handleUpdateTask,
      handleDeleteTask,
      path,
    };
  },
};
</script>

<style lang="scss" scoped>
@import "~@/assets/sass/components/_PxTask.scss";
</style>
