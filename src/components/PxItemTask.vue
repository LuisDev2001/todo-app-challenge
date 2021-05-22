<template>
  <li class="result-todo__item" v-for="(item, index) in itemsTodo" :key="index">
    <div class="checkbox">
      <input type="checkbox" v-model="checked" ref="jsCheckbox" />
      <label>
        <font-awesome-icon icon="check" />
      </label>
    </div>
    <span
      :class="{
        'result-todo__text': true,
        'is-checked': checked,
      }"
      v-text="item.task"
    >
    </span>
  </li>
</template>

<script>
import { library } from "@fortawesome/fontawesome-svg-core";
import { faCheck } from "@fortawesome/free-solid-svg-icons";
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
library.add(faCheck);

import { reactive, toRefs } from "vue";

export default {
  name: "PxItemTask",
  components: {
    FontAwesomeIcon,
  },
  props: {
    itemsTodo: Object,
  },
  setup() {
    const checkBoxState = reactive({
      checked: false,
    });

    const check = (event) => {
      // if (event.target.checked) {
      //   checkBoxState.checked = true;
      // } else {
      //   checkBoxState.checked = false;
      // }
    };

    return {
      check,
      ...toRefs(checkBoxState),
    };
  },
};
</script>

<style lang="scss" scoped>
@import "~@/assets/sass/components/_PxItemTask.scss";
</style>
