<template>
  <div class="task">
    <div class="checkbox">
      <input type="checkbox" v-model="checkBoxState" />
      <label>
        <font-awesome-icon icon="check" />
      </label>
    </div>
    <span
      :class="{
        'result-todo__text': true,
        'is-checked': checkBoxState,
      }"
      v-text="taskText"
    >
    </span>
  </div>
</template>

<script>
import { library } from "@fortawesome/fontawesome-svg-core";
import { faCheck } from "@fortawesome/free-solid-svg-icons";
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
library.add(faCheck);

export default {
  name: "PxTask",
  components: {
    FontAwesomeIcon,
  },
  props: {
    taskText: String,
    checkBoxState: Boolean,
  },
};
</script>

<style lang="scss" scoped>
.result-todo {
  .task {
    display: flex;
    align-items: center;
    justify-content: flex-start;
    font-family: "Montserrat-Medium";
    font-size: 18px;
    color: #000000;
  }
  &__text {
    &.is-checked {
      text-decoration: line-through;
    }
  }
  .checkbox {
    margin: 0 7px 0 0;
    position: relative;
    label {
      display: flex;
      align-items: center;
      justify-content: center;
      width: 24px;
      height: 24px;
      border-radius: 4px;
      border: 1px solid #828282;
      padding: 0;
      margin: 0;
      transition: 0.3s ease all;
      svg {
        font-size: 14px;
        opacity: 0;
        color: #ffffff;
        transition: 0.3s ease all;
      }
    }
    input[type="checkbox"] {
      position: absolute;
      opacity: 0;
      width: 100%;
      height: 100%;
      z-index: 1;
      &:checked ~ label {
        background: #2f80ed;
        svg {
          opacity: 1;
        }
      }
    }
  }
}
</style>
