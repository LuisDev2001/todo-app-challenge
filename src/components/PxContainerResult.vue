<template>
  <section class="result-todo">
    <ul class="result-todo__list">
      <PxItemTask :itemsTodo="dataTask" />
    </ul>
  </section>
</template>

<script>
import PxItemTask from "@/components/PxItemTask";
import { computed, onMounted, reactive, toRefs } from "vue";

export default {
  name: "PxContainerResult",
  components: {
    PxItemTask,
  },
  props: {
    itemsTodo: Object,
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

<style lang="scss" scoped>
@import "~@/assets/sass/components/_PxContainerResult.scss";
</style>
