<script setup>
const props = defineProps(["keyId", "hue"]);
</script>

<style scoped>
.brace {
  color: oklch(0.61 0.14 v-bind("props.hue"));
  font-size: larger;
}

.key {
  vertical-align: super;
  font-style: italic;
  font-size: smaller;
  color: oklch(0.61 0.14 v-bind("props.hue"));
  margin-left: 0.15em;
}
</style>

<template>
  <span class="brace">&#123;</span>
  <span class="content"><slot /></span>
  <span class="brace">&#125;</span>
  <span class="key">{{ props.keyId }}</span>
</template>
