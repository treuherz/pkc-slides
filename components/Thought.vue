<script setup>
import { computed, ref } from "vue";
const props = defineProps(["sender", "side", "hue"]);
const left = computed(() => (props?.side ?? "left") === "left");
const sideDependent = computed(() => ({
  rowJustify: left.value ? "left" : "right",
}));
</script>

<style scoped>
.row {
  display: flex;
  justify-content: v-bind("sideDependent.rowJustify");
  text-align: v-bind("sideDependent.rowJustify");

  font-style: italic;
  margin-bottom: 0.1em;
}

.sender {
  color: oklch(0.61 0.14 v-bind("props.hue"));
}

:deep(span.content em) {
  font-style: normal;
}

:deep(span.content) {
}
</style>

<template>
  <div class="row">
    <div>
      <span class="sender">{{ props.sender }}</span>
      {{}}
      <span class="content"> <slot /> </span>
    </div>
  </div>
</template>
