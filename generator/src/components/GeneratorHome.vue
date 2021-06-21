<template>
  <div class="d-flex justify-content-center">
    <div class="rounded-3 bg-midnightblue text-white p-3 shadow-lg">
      <div class="fw-bold fs-3">Password Generator</div>
      <div class="rounded-3 bg-darkblue p-3">
        <div v-if="state.button" class="fs-4">Choose Options</div>
        <div class="spinner-border" role="status" v-else>
          <span class="visually-hidden">Loading...</span>
        </div>
      </div>

      <div class="text-start small mt-3">Length:</div>
      <div class="bg-darkblue pt-3 pb-2 pe-2 ps-2 rounded-3">
        <input type="range" class="form-range" min="4" max="32" />
      </div>
      <div class="text-start small mt-3">
        Settings:
      </div>
      <SettingButton
        v-for="(setting, index) in state.settings"
        :key="index"
        :setting="setting"
      ></SettingButton>
      <button
        type="button"
        class="btn btn-secondary mt-3"
        @click="generatePassword()"
      >
        GENERATE PASSWORD
      </button>
    </div>
  </div>
</template>

<script>
import SettingButton from "./SettingButton.vue";
import { defineComponent, reactive } from "vue";
export default defineComponent({
  name: "GeneratorHome",
  components: {
    SettingButton,
  },
  setup() {
    //datas
    const state = reactive({
      settings: [
        {
          name: "Uppercase",
          isCheck: false,
        },
        {
          name: "Lowercase",
          isCheck: false,
        },
        {
          name: "Numbers",
          isCheck: false,
        },
        {
          name: "Symbols",
          isCheck: false,
        },
      ],
      button: true,
    });
    const generatePassword = () => {
      state.button = !state.button;
    };
    return { state, generatePassword };
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
.bg-midnightblue {
  background-color: #191970;
}
.bg-royalblue {
  background-color: #4169e1;
}
.bg-darkblue {
  background-color: #043c78;
}
</style>
