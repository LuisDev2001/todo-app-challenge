<template>
  <li class="result-todo__item" v-for="(item, index) in itemsTodo" :key="index">
    <PxChecboxTask :taskText="item.task" />
  </li>
</template>

<script>
import { reactive, ref, toRefs } from "vue";

import PxChecboxTask from "@/components/PxChecboxTask";
export default {
  name: "PxItemTask",
  components: {
    PxChecboxTask,
  },
  props: {
    itemsTodo: Object,
  },
  setup() {},
};
</script>

<style lang="scss" scoped>
@import "~@/assets/sass/components/_PxItemTask.scss";
</style>
