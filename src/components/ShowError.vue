<template>
  <span class="errorText">{{ errorText }}</span>
</template>

<script>
export default {
  name: "ShowError",
  props: {
    errorText: String,
  },
};
</script>

<style scoped>
.errorText {
  padding: 2px 2px 3px 5px;
  color: #dc3545;
  font-size: 0.8em;
  border-radius: 5px;
}
</style>