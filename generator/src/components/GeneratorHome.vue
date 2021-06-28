<template>
  <div class="row justify-content-center">
    <div class="col-6  text-white fw-bold p-3 shadow-main border border-hot">
      <h1 class="fw-bold fs-3 ">Password Generator</h1>

      <place-displayed-cipher
        :msg="state.msg"
        :passwordFlag="state.passwordFlag"
      ></place-displayed-cipher>

      <h2 class="text-start small mt-3">
        Length:<span class="fs-6 fw-bold">{{ state.length }}</span>
      </h2>
      <place-displayed-range-slider
        v-model.number="state.length"
      ></place-displayed-range-slider>

      <h2 class="text-start small mt-3">
        Settings:
      </h2>
      <setting-button
        @changeRadio="changeIsCheck"
        v-for="(setting, index) in state.settings"
        :key="index"
        :setting="setting"
        :index="index"
      ></setting-button>

      <button
        type="button"
        class="btn bg-hot mt-3 text-white"
        @click="showPassword(state.length)"
      >
        GENERATE PASSWORD
      </button>
    </div>
  </div>
</template>

<script>
import SettingButton from "./SettingButton.vue";
import PlaceDisplayedCipher from "./PlaceDisplayedCipher.vue";
import PlaceDisplayedRangeSlider from "./PlaceDisplayedRangeSlider.vue";
import { defineComponent, reactive } from "vue";
export default defineComponent({
  name: "GeneratorHome",
  components: {
    SettingButton,
    PlaceDisplayedCipher,
    PlaceDisplayedRangeSlider,
  },
  setup() {
    //datas
    const state = reactive({
      settings: [
        {
          name: "Uppercase",
          isCheck: false,
          string: "ABCDEFGHIJKLMNOPQRSTUVWXYZ",
        },
        {
          name: "Lowercase",
          isCheck: false,
          string: "abcdefghijklmnopqrstuvwxyz",
        },
        {
          name: "Numbers",
          isCheck: false,
          string: "1234567890",
        },
        {
          name: "Symbols",
          isCheck: false,
          string: "#$%(){}@!?",
        },
      ],
      passwordFlag: "A",
      msg: "init",
      length: 18,
    });
    const changeIsCheck = (...args) => {
      state.settings[args[0]].isCheck = args[1];
    };
    const showPassword = (length) => {
      state.passwordFlag = "B";
      state.msg = generatePassword(length) || "Please Choose Settings";
      setTimeout(() => (state.passwordFlag = "C"), 700);
    };
    const generatePassword = (length) => {
      let cipherGenerateString = "";
      //パスワードを生成するためのもとの文字列を生成。
      state.settings.forEach(
        (setting) => setting.isCheck && (cipherGenerateString += setting.string)
      );
      //パスワードの生成
      let result = "";
      for (let i = 0; i < length; i++) {
        if (!cipherGenerateString) break;
        result +=
          cipherGenerateString[
            Math.floor(Math.random() * (cipherGenerateString.length - 1))
          ];
      }
      return result;
    };
    return { state, showPassword, changeIsCheck };
  },
});
</script>

<style scoped>
.bg-main {
  background-color: #15202b;
}
.bg-hot {
  background-color: #ff5311;
}
.border-hot {
  border-color: #ff5311 !important;
}
.shadow-main {
  border-radius: 46px;
  background: #15202b;
  box-shadow: 36px 36px 0px #080d11, -36px -36px 0px #223345;
}
.shadow-hot {
  border-radius: 50px;
  background: #1a91da;
  box-shadow: 20px 20px 60px #167bb9, -20px -20px 60px #1ea7fb;
}
</style>
