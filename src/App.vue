<template>
  <h1 class="main-title">#todo</h1>
  <PxHeader />
  <PxFormTask />
  <router-view />
</template>

<script>
import PxHeader from "@/components/PxHeader";
import PxFormTask from "@/components/PxFormTask";

export default {
  components: {
    PxHeader,
    PxFormTask,
  },
};
</script>

<style lang="scss">
@import "~@/assets/sass/_base.scss";
#app {
  width: 100%;
  max-width: 610px;
  margin: 0 auto;
  padding: 0 15px;
}
</style>
