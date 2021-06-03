<template>
  <div class="detele__all" v-if="dataTask.length > 0">
    <PxAlert
      :activeAlert="isOpen"
      :activeSucces="success"
      :activeInfo="info"
      :activeError="error"
      :activeWarn="warning"
      :alertText="text"
    />
    <button class="detele__all-btn" @click="handleDeleteAllTask()">
      <font-awesome-icon icon="trash-alt" />
      delete all
    </button>
  </div>
</template>

<script>
import { ref, inject, reactive, toRefs } from "vue";

import { library } from "@fortawesome/fontawesome-svg-core";
import { faTrashAlt } from "@fortawesome/free-solid-svg-icons";
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
library.add(faTrashAlt);

import PxAlert from "@/components/PxAlert";

export default {
  name: "PxBtnDeleteCompletedTask",
  components: {
    FontAwesomeIcon,
    PxAlert,
  },
  setup() {
    const dataTask = inject("dataTodoListState");
    const alertState = reactive({
      isOpen: false,
      success: false,
      error: false,
      warning: false,
      info: false,
      text: "",
    });

    const handleDeleteAllTask = async () => {
      dataTask.value.forEach(async (task) => {
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
          alertState.text = "All tasks were deleted";
          setTimeout(() => {
            alertState.isOpen = false;
            alertState.success = false;
          }, 3000);

          const newTaskListDeleteAll = dataTask.value.filter((task) => {
            return task.status != true;
          });
          setTimeout(() => {
            dataTask.value = newTaskListDeleteAll;
          }, 2000);
        } catch (error) {
          console.log(error);
        }
      });
    };

    return {
      handleDeleteAllTask,
      dataTask,
      ...toRefs(alertState),
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
