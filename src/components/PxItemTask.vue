<template>
  <li class="result-todo__item" v-for="(item, index) in dataTask" :key="index">
    <PxTask
      :idTask="item.id"
      :taskText="item.task"
      :checkBoxState="item.status"
    />
    <div v-if="path == '/completed-task'" class="result-todo__delete">
      <font-awesome-icon icon="trash-alt" />
    </div>
  </li>
</template>

<script>
import { inject, watchEffect } from "vue";
import { useRoute } from "vue-router";

import { library } from "@fortawesome/fontawesome-svg-core";
import { faTrashAlt } from "@fortawesome/free-solid-svg-icons";
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
library.add(faTrashAlt);

import PxTask from "@/components/PxTask";

export default {
  name: "PxItemTask",
  components: {
    PxTask,
    FontAwesomeIcon,
  },
  setup() {
    const dataTask = inject("dataTodoListState");
    const path = useRoute().path;

    return {
      dataTask,
      path,
    };
  },
};
</script>

<style lang="scss" scoped>
@import "~@/assets/sass/components/_PxItemTask.scss";
</style>
