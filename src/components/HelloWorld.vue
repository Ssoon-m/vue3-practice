<template>
  <div class="greetings">
    <h1 @click="counterStore.increment" class="green">{{ message }}</h1>
    <h2>{{ countState }}</h2>
    <h3>
      You’ve successfully created a project with
      <a target="_blank" href="https://vitejs.dev/">Vite</a> +
      <a target="_blank" href="https://vuejs.org/">Vue 3</a>. What's next?
    </h3>
  </div>
</template>

<script lang="ts">
import { ref, toRefs, toRef, onMounted, computed } from "vue";

import { useCounterStore } from "../stores/counter";

export default {
  props: {
    msg: String,
  },
  setup(props) {
    onMounted(() => {
      console.log("mounted~~~~");
    });
    // counter 를 구조분해시에 store state의 반응성을 잃는다.
    const counterStore = useCounterStore();
    // 만약 useCounterStore저네 말고 기존과 같이 computed를 사용할때
    const countState = computed(() => counterStore.doubleCount);
    // setup에 {msg} 이렇게 인자로 받는건 안된다.
    // 구조분해시 반응성을 유지하려면 toRefs 사용
    // 만약 store 에서 사용하고 싶으면 storeToRefs
    const { msg } = toRefs(props);
    const message = msg.value;

    const count = ref(10);
    const computedCount = computed(() => count.value * 2);
    const increment = () => {
      count.value++;
    };

    return {
      count,
      message,
      increment,
      computedCount,
      counterStore,
      countState,
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
