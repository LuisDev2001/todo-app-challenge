<template>
  <section class="active">
    <PxFormTask />

    <PxContainerResult :itemsTodo="dataTodoListState" />
  </section>
</template>

<script>
import { onMounted, ref, provide } from "vue";

import PxContainerResult from "@/components/PxContainerResult";
import PxFormTask from "@/components/PxFormTask";

export default {
  name: "ActiveTask",
  components: {
    PxContainerResult,
    PxFormTask,
  },
  setup() {
    const dataTodoListState = ref([]);
    provide("dataTodoListState", dataTodoListState);

    const getAllActiveTask = async () => {
      try {
        const API = "https://api-fake-todo-app-2021.herokuapp.com/task";
        const getData = await fetch(API);
        const response = await getData.json();
        for (const task of response) {
          if (!task.status) {
            dataTodoListState.value.push(task);
          }
        }
      } catch (error) {
        console.log(error);
      }
    };

    onMounted(async () => await getAllActiveTask());

    return {
      dataTodoListState,
    };
  },
};
</script>

<style></style>
