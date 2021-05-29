<template>
  <section class="result-todo">
    <ul class="result-todo__list">
      <PxEmptyTask v-if="dataTask.length == 0" />
      <PxItemTask v-else />
    </ul>
  </section>
</template>

<script>
import { inject, onMounted, ref } from "vue";

import PxItemTask from "@/components/PxItemTask";
import PxEmptyTask from "@/components/PxEmptyTask";

export default {
  name: "PxContainerResult",
  components: {
    PxItemTask,
    PxEmptyTask,
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
@import "~@/assets/sass/components/_PxContainerResult.scss";
</style>
