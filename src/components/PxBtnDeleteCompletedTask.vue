<template>
  <div class="detele__all">
    <button class="detele__all-btn">
      <font-awesome-icon icon="trash-alt" />
      delete all
    </button>
  </div>
</template>

<script>
import { library } from "@fortawesome/fontawesome-svg-core";
import { faTrashAlt } from "@fortawesome/free-solid-svg-icons";
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
library.add(faTrashAlt);

export default {
  name: "PxBtnDeleteCompletedTask",
  components: {
    FontAwesomeIcon,
  },
};
</script>

<style lang="scss" scoped>
.detele__all {
  width: 100%;
  text-align: right;
  margin: 32px 0 0 0;
  &-btn {
    width: 124px;
    height: 40px;
    border-radius: 4px;
    background: #eb5757;
    color: #ffffff;
    border: 1px solid #eb5757;
    margin: 0;
    padding: 0;
    font-size: 12px;
    font-family: "Montserrat-Medium";
    transition: 0.4s ease all;
    svg {
      margin: 0 5.5px 0 0;
      font-size: 12px;
    }
    &:hover {
      background: #ffffff;
      color: #eb5757;
    }
  }
}
</style>
