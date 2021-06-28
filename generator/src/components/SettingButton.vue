<template>
  <div class="border border-hot form-switch p-2 m-1 rounded-3 ">
    <div class="d-flex justify-content-between">
      <label for="radio" class="fs-6 pt-1">Include {{ setting.name }}</label>
      <input
        @change="changeCheckBox"
        id="radio"
        class="form-check-input me-2"
        type="checkbox"
        v-model="state.checked"
      />
    </div>
  </div>
</template>

<script>
import { defineComponent, reactive } from "vue";
export default defineComponent({
  name: "SettingBuuton",
  props: {
    setting: {
      type: Object,
      default: () => ({
        name: "setting_name",
        isCheck: false,
        string: "cipherString",
      }),
    },
    index: {
      type: Number,
      default: 0,
    },
  },
  setup(props, context) {
    const state = reactive({
      checked: false,
    });
    const changeCheckBox = () => {
      context.emit("changeRadio", props.index, state.checked);
    };

    return { state, changeCheckBox };
  },
});
</script>

<style>
.form-check-input {
  transform: scale(1.3);
}
.border-hot {
  border-color: #ff5311 !important;
}
</style>
