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
    <PxAlert
      :activeAlert="isOpen"
      :activeSucces="success"
      :activeInfo="info"
      :activeError="error"
      :activeWarn="warning"
      :alertText="text"
    />
  </form>
</template>

<script>
import PxAlert from "@/components/PxAlert";

import { inject, reactive, ref, toRefs } from "vue";
import { faCheck } from "@fortawesome/free-solid-svg-icons";
export default {
  name: "PxFormTask",
  components: {
    PxAlert,
  },
  setup(props) {
    let task = ref("");

    const alertState = reactive({
      isOpen: false,
      success: false,
      error: false,
      warning: false,
      info: false,
      text: "",
    });

    const dataTodo = inject("dataTodoListState");

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
              alertState.isOpen = true;
              alertState.error = true;
              alertState.text = "Service connection error";
              setTimeout(() => {
                alertState.isOpen = false;
                alertState.error = false;
              }, 4000);
              //Clean input task
              task.value = "";
              return false;
            }
          }

          const data = await response.json();
          dataTodo.value.push(data);
          task.value = "";
          alertState.isOpen = true;
          alertState.success = true;
          alertState.text = "Task added correctly!";
          setTimeout(() => {
            alertState.isOpen = false;
            alertState.success = false;
          }, 4000);
        } catch (error) {
          console.error(error);
        }
      } else {
        alertState.isOpen = true;
        alertState.info = true;
        alertState.text = "Enter a task, please";
        setTimeout(() => {
          alertState.isOpen = false;
          alertState.info = false;
        }, 4000);
      }
    };

    return {
      submitTask,
      task,
      ...toRefs(alertState),
    };
  },
};
</script>

<style lang="scss" scoped>
@import "~@/assets/sass/components/_PxFormTask.scss";
</style>
