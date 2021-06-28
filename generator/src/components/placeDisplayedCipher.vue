<template>
  <div
    class="rounded-3 p-3 border
        border-hot"
  >
    <div v-if="passwordFlag === 'A'" class="fs-4">Choose Settings</div>
    <div class="spinner-border" role="status" v-else-if="passwordFlag === 'B'">
      <div class="visually-hidden">Loading...</div>
    </div>
    <div class="fs-4" v-else>{{ msg }}</div>
  </div>
</template>

<script>
import { defineComponent } from "vue";
export default defineComponent({
  neme: "placeDisplayedCipher",
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
