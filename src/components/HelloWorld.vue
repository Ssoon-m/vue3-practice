<template>
  <div class="greetings">
    <h1 class="green">{{ message }}</h1>
    <h2>{{ count }}</h2>
    <h3>
      You’ve successfully created a project with
      <a target="_blank" href="https://vitejs.dev/">Vite</a> +
      <a target="_blank" href="https://vuejs.org/">Vue 3</a>. What's next?
    </h3>
  </div>
</template>

<script lang="ts">
import { ref, toRefs, toRef } from 'vue';

interface Props {
  msg: string;
}

// const props = defineProps<Props>();

export default {
  props: {
    msg: String,
  },
  setup(props) {
    const { msg } = toRefs(props);

    const count = ref(0);
    const message = msg.value;
    return {
      count,
      message,
    };
  },
};
</script>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
