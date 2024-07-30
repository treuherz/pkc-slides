<script setup>
const props = defineProps(["hue"]);
</script>

<style scoped>
.content {
  color: oklch(0.61 0.14 v-bind("props.hue"));
}
</style>

<template>
  <span class="content"
    ><em><slot /></em
  ></span>
</template>
