<template>
  <div class="counter">
    <div>счетчик = {{ counter }}</div>
    <button @click="changeCounter(1)">+</button>
    <button @click="changeCounter(-1)">-</button>
  </div>
</template>
<script lang="ts">
import { Vue, Options } from "vue-class-component";
@Options<Counter>({
  props: {
    modelValue: { type: Number, default: 1 },
  },
  watch: {
    counter(value: 0) {
      this.$emit("update:modelValue", Number(this.counter));
    },
    modelValue(value) {
      this.counter = this.modelValue;
    },
  },
  emits: ["update:modelValue"],
})
export default class Counter extends Vue {
  readonly modelValue: number = 0;
  counter = 0;
  mounted() {
    this.counter = this.modelValue;
  }
  changeCounter(value: number = 1) {
    this.counter += value;
  }
}
</script>
<style lang="less">
.counter {
  padding: 10px;
  background: orange;
}
</style>