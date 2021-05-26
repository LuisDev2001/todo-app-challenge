<template>
  <section class="completed">
    <PxContainerResult :itemsTodo="dataCompletedTask" />
  </section>
</template>

<script>
import { onMounted, reactive, toRefs } from "vue";

import PxContainerResult from "@/components/PxContainerResult";

export default {
  name: "CompletedTask",
  components: {
    PxContainerResult,
  },
  setup() {
    const dataTodoListCompletedState = reactive({
      dataCompletedTask: [],
    });

    const getAllCompletedTask = async () => {
      try {
        const API = "https://api-fake-todo-app-2021.herokuapp.com/task";
        const getData = await fetch(API);
        const response = await getData.json();
        for (const task of response) {
          if (task.status) {
            dataTodoListCompletedState.dataCompletedTask.push(task);
          }
        }
      } catch (error) {
        console.log(error);
      }
    };

    onMounted(async () => {
      await getAllCompletedTask();
    });

    return {
      ...toRefs(dataTodoListCompletedState),
    };
  },
};
</script>

<style></style>
