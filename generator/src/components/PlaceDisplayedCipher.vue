<template>
  <div
    class="rounded-3 p-3 border
        border-hot"
  >
    <div v-if="passwordFlag === 'A'" class="fs-4">Choose Settings</div>
    <div v-else-if="passwordFlag === 'B'" class="spinner-border" role="status">
      <div class="visually-hidden">Loading...</div>
    </div>
    <div v-else class="fs-4">{{ msg }}</div>
  </div>
</template>

<script>
import { defineComponent } from "vue";
export default defineComponent({
  neme: "PlaceDisplayedCipher",
  props: {
    msg: {
      type: String,
      default: "init",
    },
    passwordFlag: {
      type: String,
      default: "A",
    },
  },
});
</script>

<style scoped>
.border-hot {
  word-break: break-all;
}
</style>
