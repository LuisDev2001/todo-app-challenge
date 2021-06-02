<template>
  <div
    :class="{
      alert: true,
      alert__error: activeError,
      alert__succes: activeSucces,
      alert__warning: activeWarn,
      alert__info: activeInfo,
      'is-open': activeAlert,
    }"
  >
    <span class="alert__icon">
      <font-awesome-icon v-if="activeSucces" icon="check-circle" />
      <font-awesome-icon v-if="activeInfo" icon="info-circle" />
      <font-awesome-icon v-if="activeError" icon="times-circle" />
      <font-awesome-icon v-if="activeWarn" icon="exclamation-circle" />
    </span>
    <p class="alert__text" v-text="alertText"></p>
  </div>
</template>

<script>
import { library } from "@fortawesome/fontawesome-svg-core";
import {
  faCheckCircle,
  faInfoCircle,
  faTimesCircle,
  faExclamationCircle,
} from "@fortawesome/free-solid-svg-icons";
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
library.add(faCheckCircle, faInfoCircle, faTimesCircle, faExclamationCircle);

export default {
  name: "PxAlert",
  props: {
    activeAlert: Boolean,
    activeError: Boolean,
    activeSucces: Boolean,
    activeWarn: Boolean,
    activeInfo: Boolean,
    alertText: String,
  },
  components: {
    FontAwesomeIcon,
  },
};
</script>

<style lang="scss" scoped>
@import "~@/assets/sass/components/_PxAlert.scss";
</style>
