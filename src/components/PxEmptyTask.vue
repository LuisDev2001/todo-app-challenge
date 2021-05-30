<template>
  <div
    :class="{
      empty__task: true,
    }"
  >
    <div class="empty__task-icon">
      <font-awesome-icon icon="tasks" />
    </div>
    <div class="empty__task-text" v-text="message"></div>
  </div>
</template>

<script>
import { library } from "@fortawesome/fontawesome-svg-core";
import { faTasks } from "@fortawesome/free-solid-svg-icons";
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import { ref } from "vue";
library.add(faTasks);

export default {
  name: "PxEmptyTask",
  components: {
    FontAwesomeIcon,
  },
  props: {
    active: Boolean,
  },
  setup() {
    const message = ref("No hay tareas, ingrese tareas al app todo list😁.");

    return {
      message,
    };
  },
};
</script>

<style lang="scss" scoped>
.empty__task {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 30px 15px;
  &-icon {
    svg {
      font-size: 45px;
      color: #2f80ed;
    }
  }
  &-text {
    font-size: 22px;
    margin: 10px 0 0;
  }
}
</style>
