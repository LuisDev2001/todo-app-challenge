<template>
  <section class="completed">
    <PxContainerResult :itemsTodo="dataTodoListState" />
  </section>
</template>

<script>
import { onMounted, provide, ref } from "vue";

import PxContainerResult from "@/components/PxContainerResult";

export default {
  name: "CompletedTask",
  components: {
    PxContainerResult,
  },
  setup() {
    const dataTodoListState = ref([]);
    provide("dataTodoListState", dataTodoListState);

    const getAllCompletedTask = async () => {
      try {
        const API = "https://api-fake-todo-app-2021.herokuapp.com/task";
        const getData = await fetch(API);
        const response = await getData.json();
        for (const task of response) {
          if (task.status) {
            dataTodoListState.value.push(task);
          }
        }
      } catch (error) {
        console.log(error);
      }
    };

    onMounted(async () => await getAllCompletedTask());

    return {
      dataTodoListState,
    };
  },
};
</script>

<style></style>
