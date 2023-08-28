<template>
  <div class="counter">
    <counter-button
      @click="decrement"
    > -
    </counter-button>
    <CounterValue
      :value="count"
    >
      Current value: {{count}}
    </CounterValue>
    <counter-button
      @action="increment"
    >
      +
    </counter-button>
  </div>
</template>

<script setup>
import {ref}  from 'vue';
import CounterButton from "./CounterButton.vue";
import CounterValue from "./CounterValue.vue";

const count = ref(0);

const decrement = () => {
  count.value = count.value - 1;
}

const increment  = () => {
  count.value = count.value + 1
}

</script>


<style lang="scss" scoped>
.counter {
  display: flex;
  align-items: center;

  button {
    margin: 0 10px;
    font-size: 1.5rem;
    width: 2rem;
    height: 2rem;
    border-radius: 50%;
    border: none;
    background: #dd0000;
    color: white;
    cursor: pointer;

    &:hover {
      background: #ff0000;
    }
  }
}
</style>
