<template>
  <h1 class="main-title">#todo</h1>
  <PxHeader />
  <router-view />
</template>

<script>
import PxHeader from "@/components/PxHeader";
export default {
  components: {
    PxHeader,
  },
};
</script>

<style lang="scss">
@import "~@/assets/sass/_base.scss";
</style>
