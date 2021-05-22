<template>
  <header class="header">
    <router-link to="/">All</router-link>
    <router-link to="/active-task">active task</router-link>
    <router-link to="/completed-task">completed task</router-link>
  </header>
</template>

<script>
export default {
  name: "PxHeader",
};
</script>

<style lang="scss" scoped></style>
