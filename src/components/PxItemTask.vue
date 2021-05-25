<template>
  <li class="result-todo__item" v-for="(item, index) in itemsTodo" :key="index">
    <PxChecboxTask :taskText="item.task" :checkBoxState="item.status" />
  </li>
</template>

<script>
import PxChecboxTask from "@/components/PxChecboxTask";
export default {
  name: "PxItemTask",
  components: {
    PxChecboxTask,
  },
  props: {
    itemsTodo: Object,
  },
};
</script>

<style lang="scss" scoped>
@import "~@/assets/sass/components/_PxItemTask.scss";
</style>
