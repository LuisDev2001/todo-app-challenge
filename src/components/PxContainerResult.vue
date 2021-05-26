<template>
  <section class="result-todo">
    <ul class="result-todo__list">
      <PxItemTask :itemsTodo="dataTask" />
    </ul>
  </section>
</template>

<script>
import PxItemTask from "@/components/PxItemTask";
import { onMounted, ref } from "vue";

export default {
  name: "PxContainerResult",
  components: {
    PxItemTask,
  },
  props: {
    itemsTodo: Array,
  },
  setup(props) {
    const dataTask = props.itemsTodo;

    return {
      dataTask,
    };
  },
};
</script>

<style lang="scss" scoped>
@import "~@/assets/sass/components/_PxContainerResult.scss";
</style>
