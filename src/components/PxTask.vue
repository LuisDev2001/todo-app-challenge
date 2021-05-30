<template>
  <div class="task">
    <div class="checkbox">
      <input type="hidden" :value="idTask" class="task-id" />
      <input
        type="checkbox"
        v-model="checkBoxState"
        @change="handleUpdateTask"
      />
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
import { ref } from "vue";

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
    idTask: Number,
  },
  setup(props) {
    let message = ref("");

    const handleUpdateTask = async () => {
      try {
        const API = "https://api-fake-todo-app-2021.herokuapp.com/task";

        const config = {
          method: "PUT",
          body: JSON.stringify({
            id: props.idTask,
            task: props.taskText,
            status: props.checkBoxState,
          }),
          headers: {
            "Content-type": "application/json; charset=UTF-8",
          },
        };

        const response = await fetch(`${API}/${props.idTask}`, config);

        // Validate status code
        if (!response.ok) {
          if (response.status == 404) {
            message.value = "Error de conexion con el servicio";
            console.error(message.value);
          }
        }
        const data = await response.json();
        console.log(`Se actualizo la tarea con el id ${props.idTask}`);
        console.log(data);
      } catch (error) {
        console.log(error);
      }
    };

    return {
      handleUpdateTask,
    };
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
