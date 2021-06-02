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
    <PxAlert
      :activeAlert="isOpen"
      :activeSucces="success"
      :activeInfo="info"
      :activeError="error"
      :activeWarn="warning"
      :alertText="text"
    />
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
import { ref, inject, toRefs, reactive } from "vue";
import { useRoute } from "vue-router";

import { library } from "@fortawesome/fontawesome-svg-core";
import { faCheck, faTrashAlt } from "@fortawesome/free-solid-svg-icons";
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";

library.add(faCheck, faTrashAlt);

import PxAlert from "@/components/PxAlert";

export default {
  name: "PxTask",
  components: {
    FontAwesomeIcon,
    PxAlert,
  },
  props: {
    taskText: String,
    checkBoxState: Boolean,
    idTask: Number,
  },
  setup(props) {
    const path = useRoute().path;
    const dataTask = inject("dataTodoListState");

    const alertState = reactive({
      isOpen: false,
      success: false,
      error: false,
      warning: false,
      info: false,
      text: "",
    });

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
            alertState.isOpen = true;
            alertState.error = true;
            alertState.text = "Service connection error";
            setTimeout(() => {
              alertState.isOpen = false;
              alertState.error = false;
            }, 3000);
            return false;
          }
        }
        const data = await response.json();
        alertState.isOpen = true;
        alertState.success = true;
        alertState.text = "Task updated successfully";
        setTimeout(() => {
          alertState.isOpen = false;
          alertState.success = false;
        }, 3000);
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
            alertState.isOpen = true;
            alertState.error = true;
            alertState.text = "Service connection error";
            setTimeout(() => {
              alertState.isOpen = false;
              alertState.error = false;
            }, 3000);
            return false;
          }
        }

        const data = await response.json();
        alertState.isOpen = true;
        alertState.success = true;
        alertState.text = "Task deleted successfully";
        setTimeout(() => {
          alertState.isOpen = false;
          alertState.success = false;
        }, 3000);

        const newTaskListCompleted = dataTask.value.filter((task) => {
          return task.id !== props.idTask;
        });
        setTimeout(() => {
          dataTask.value = newTaskListCompleted;
        }, 2000);
      } catch (error) {
        console.log(error);
      }
    };

    return {
      handleUpdateTask,
      handleDeleteTask,
      path,
      ...toRefs(alertState),
    };
  },
};
</script>

<style lang="scss" scoped>
@import "~@/assets/sass/components/_PxTask.scss";
</style>
