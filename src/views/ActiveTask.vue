<template>
  <section class="active">
    <PxContainerResult :itemsTodo="dataActiveTask" />
  </section>
</template>

<script>
import PxContainerResult from "@/components/PxContainerResult";
import { reactive, onMounted, toRefs } from "vue";

export default {
  name: "ActiveTask",
  components: {
    PxContainerResult,
  },
  setup() {
    const dataTodoListActiveState = reactive({
      dataActiveTask: [],
    });

    const getAllActiveTask = async () => {
      try {
        const API = "https://api-fake-todo-app-2021.herokuapp.com/task";
        const getData = await fetch(API);
        const response = await getData.json();
        for (const task of response) {
          if (!task.status) {
            dataTodoListActiveState.dataActiveTask.push(task);
          }
        }
      } catch (error) {
        console.log(error);
      }
    };

    onMounted(async () => {
      await getAllActiveTask();
    });

    return {
      ...toRefs(dataTodoListActiveState),
    };
  },
};
</script>

<style></style>
