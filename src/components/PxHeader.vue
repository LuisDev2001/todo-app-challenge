<template>
  <header class="header">
    <nav class="menu">
      <ul class="menu__list">
        <li class="menu__item" v-for="(link, index) in links" :key="index">
          <router-link
            :to="link.to"
            class="menu__link"
            v-text="link.linkText"
          ></router-link>
        </li>
      </ul>
    </nav>
  </header>
</template>

<script>
import { reactive, toRefs } from "vue";
export default {
  name: "PxHeader",
  setup() {
    //Array of objects for header link
    const linksMenuState = reactive({
      links: [
        {
          to: "/",
          linkText: "All",
        },
        {
          to: "/active-task",
          linkText: "Active",
        },
        {
          to: "/completed-task",
          linkText: "Completed",
        },
      ],
    });

    return {
      ...toRefs(linksMenuState),
    };
  },
};
</script>

<style lang="scss" scoped>
@import "~@/assets/sass/components/_PxHeader.scss";
</style>
