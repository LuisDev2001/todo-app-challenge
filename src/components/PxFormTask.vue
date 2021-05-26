<template>
  <form action="" class="form" @submit.prevent="submitTask">
    <div class="form-group input">
      <input
        type="text"
        autocomplete="off"
        placeholder="Add details"
        v-model="task"
      />
    </div>
    <div class="form-group">
      <button type="submit">Add</button>
    </div>
  </form>
</template>

<script>
import { ref } from "vue";
export default {
  name: "PxFormTask",
  setup() {
    let task = ref("");

    const submitTask = async () => {
      try {
        const API = "https://api-fake-todo-app-2021.herokuapp.com/task";
        const config = {
          method: "POST",
          body: JSON.stringify({
            task: task.value,
            status: false,
          }),
          headers: {
            "Content-type": "application/json; charset=UTF-8",
          },
        };
        const response = await fetch(API, config);
        const data = await response.json();
        task.value = "";
        console.log(data);
      } catch (error) {
        console.log(error);
      }
    };

    return {
      submitTask,
      task,
    };
  },
};
</script>

<style lang="scss" scoped>
@import "~@/assets/sass/components/_PxFormTask.scss";
</style>
