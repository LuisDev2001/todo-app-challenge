<template>
  <div class="all">
    <PxFormTask />
    <PxContainerResult />
  </div>
</template>

<script>
import { onMounted, provide, ref, watchEffect } from "vue";

// @ is an alias to /src
import PxContainerResult from "@/components/PxContainerResult";
import PxFormTask from "@/components/PxFormTask";

export default {
  name: "Home",
  components: {
    PxContainerResult,
    PxFormTask,
  },
  setup() {
    const dataTodoListState = ref([]);

    provide("dataTodoListState", dataTodoListState);

    const getAllTask = async () => {
      try {
        const API = "https://api-fake-todo-app-2021.herokuapp.com/task";
        const getData = await fetch(API);
        const response = await getData.json();
        for (const task of response) {
          dataTodoListState.value.push(task);
        }
      } catch (error) {
        console.log(error);
      }
    };

    watchEffect(() => {
      // console.log(dataTodoListState.value.length);
      // console.log(dataTodoListState.value);
    });

    onMounted(async () => await getAllTask());

    return {
      dataTodoListState,
    };
  },
};
</script>
