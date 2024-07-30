<script setup>
import { computed } from "vue";
const props = defineProps(["sender", "tag", "side", "hue"]);
const left = computed(() => (props?.side ?? "left") === "left");
const sideDependent = computed(() => ({
  rowJustify: left.value ? "left" : "right",
  senderJustify: left.value ? "right" : "left",
  areas: left.value
    ? ['". tag ." "sender content ."']
    : ['". tag ." ". content sender"'],
  border: left.value ? "0 0 0 2px" : "0 2px 0 0",
}));
</script>

<style scoped>
.row {
  display: flex;
  justify-content: v-bind("sideDependent.rowJustify");
  margin-bottom: 0.2em;
}

.layout {
  display: grid;
  width: fit-content;
  grid-template-columns: 2em auto 2em;
  grid-template-areas: v-bind("sideDependent.areas");
}

.sender {
  grid-area: sender;
  justify-self: v-bind("sideDependent.senderJustify");

  color: oklch(0.61 0.14 v-bind("props.hue"));
  padding: 0 0.4em;
}

.tag {
  grid-area: tag;
  justify-self: left;

  font-family: monospace;
  font-style: italic;
  font-size: 0.6em;

  color: #999;
}

.content {
  grid-area: content;
  align-content: center;

  font-family: "Avenir Next";
  padding: 0 0.4em;

  background-color: oklch(0.94 0.07 v-bind("props.hue"));
  border-color: oklch(0.61 0.14 v-bind("props.hue"));
  border-width: v-bind("sideDependent.border");
}

:deep(p) {
  margin-top: 0.1em;
  margin-bottom: 0.1em;
  line-height: 1.2em;
}
</style>

<template>
  <div class="row">
    <div class="layout">
      <div class="sender">{{ props.sender }}</div>
      <div class="tag">{{ props.tag }}</div>
      <div class="content">
        <p><slot /></p>
      </div>
    </div>
  </div>
</template>
