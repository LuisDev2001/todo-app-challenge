<template>
  <div class="all">
    <PxContainerResult :itemsTodo="dataTask" />
  </div>
</template>

<script>
import { computed, onMounted, reactive, toRefs } from "vue";

// @ is an alias to /src
import PxContainerResult from "@/components/PxContainerResult";

export default {
  name: "Home",
  components: {
    PxContainerResult,
  },
  setup() {
    const dataTodoListState = reactive({
      dataTask: [],
    });

    const getAllTask = async () => {
      try {
        const API = "https://api-fake-todo-app-2021.herokuapp.com/task";
        const getData = await fetch(API);
        const response = await getData.json();
        for (const task of response) {
          dataTodoListState.dataTask.push(task);
        }
      } catch (error) {
        console.log(error);
      }
    };

    onMounted(async () => {
      await getAllTask();
    });

    return {
      ...toRefs(dataTodoListState),
    };
  },
};
</script>
