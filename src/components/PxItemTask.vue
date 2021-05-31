<template>
  <li class="result-todo__item" v-for="(item, index) in dataTask" :key="index">
    <PxTask
      :idTask="item.id"
      :taskText="item.task"
      :checkBoxState="item.status"
    />
  </li>
</template>

<script>
import { inject } from "vue";

import PxTask from "@/components/PxTask";

export default {
  name: "PxItemTask",
  components: {
    PxTask,
  },
  setup() {
    const dataTask = inject("dataTodoListState");

    return {
      dataTask,
    };
  },
};
</script>

<style lang="scss" scoped>
@import "~@/assets/sass/components/_PxItemTask.scss";
</style>
