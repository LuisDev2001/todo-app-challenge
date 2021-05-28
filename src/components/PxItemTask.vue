<template>
  <li class="result-todo__item" v-for="(item, index) in dataTask" :key="index">
    <PxChecboxTask :taskText="item.task" :checkBoxState="item.status" />
  </li>
</template>

<script>
import PxChecboxTask from "@/components/PxChecboxTask";
import { inject } from "vue";
export default {
  name: "PxItemTask",
  components: {
    PxChecboxTask,
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
