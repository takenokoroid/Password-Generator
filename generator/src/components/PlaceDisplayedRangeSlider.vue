<template>
  <div class="border border-hot pt-3 pb-2 pe-2 ps-2 rounded-3">
    <label for="customRange2" class="form-label"></label>
    <input
      type="range"
      class="form-range"
      min="4"
      max="32"
      v-model.number="state.length"
      @change="changeRangeSlider"
    />
  </div>
</template>

<script>
import { defineComponent, reactive } from "vue";
export default defineComponent({
  name: "PlaceDisplayRangeSlider",
  props: {
    length: {
      type: Number,
      default: 18,
    },
    modelValue: Number,
  },
  setup(props, context) {
    const state = reactive({
      length: 18,
    });
    const changeRangeSlider = () => {
      console.log(state.length);
      context.emit("update:modelValue", state.length);
    };
    return { state, changeRangeSlider };
  },
});
</script>

<style scoped>
.form-range::-webkit-slider-thumb {
  background: #fff;
}
.form-range::-moz-slider-thumb {
  background: #fff;
}
</style>
