<template>
  <div class="bg-darkblue form-switch p-2 m-1 rounded-3 ">
    <div class="d-flex justify-content-between">
      <div class="">Include {{ setting.name }}</div>
      <input class="form-check-input me-2" type="checkbox" />
    </div>
  </div>
</template>

<script>
import { defineComponent } from "vue";
export default defineComponent({
  name: "SettingBuuton",
  props: {
    setting: {
      type: Object,
      default: () => ({
        name: "setting_name",
        isCheck: false,
      }),
    },
  },
  setup() {},
});
</script>

<style>
.form-check-input {
  transform: scale(1.3);
}
.bg-darkblue {
  background-color: #043c78;
}
</style>
