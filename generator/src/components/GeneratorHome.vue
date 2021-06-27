<template>
  <div class="row justify-content-center">
    <div class="col-6  text-white fw-bold p-3 shadow-main">
      <div class="fw-bold fs-3 ">Password Generator</div>
      <div class="rounded-3 border border-hot p-3 ">
        <div v-if="state.passwordFlag === 'A'" class="fs-4">Choose Options</div>
        <div
          class="spinner-border"
          role="status"
          v-else-if="state.passwordFlag === 'B'"
        >
          <div class="visually-hidden">Loading...</div>
        </div>
        <div class="fs-4" v-else>{{ state.msg }}</div>
      </div>

      <div class="text-start small mt-3">
        Length:<span class="fs-6 fw-bold">{{ state.length }}</span>
      </div>
      <div class="border border-hot pt-3 pb-2 pe-2 ps-2 rounded-3">
        <label for="customRange2" class="form-label"></label>
        <input
          type="range"
          class="form-range"
          v-model.number="state.length"
          min="4"
          max="32"
        />
      </div>
      <div class="text-start small mt-3">
        Settings:
      </div>
      <SettingButton
        @changeRadio="changeIsCheck"
        v-for="(setting, index) in state.settings"
        :key="index"
        :setting="setting"
        :index="index"
      ></SettingButton>
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
      const types = {
        upper: "ABCDEFGHIJKLMNOPQRSTUVWXYZ",
        lower: "abcdefghijklmnopqrstuvwxyz",
        number: "1234567890",
        symbol: "#$%(){}@!?",
      };
      let cipherGenerateString = "";
      //パスワードを生成するためのもとの文字列を生成。settingで回したほうがきれいにできそう
      if (state.settings[0].isCheck) cipherGenerateString += types.upper;
      if (state.settings[1].isCheck) cipherGenerateString += types.lower;
      if (state.settings[2].isCheck) cipherGenerateString += types.number;
      if (state.settings[3].isCheck) cipherGenerateString += types.symbol;

      // パスワードの生成
      let result = "";
      if (cipherGenerateString !== "") {
        for (let i = 0; i < length; i++) {
          result +=
            cipherGenerateString[
              Math.floor(Math.random() * (cipherGenerateString.length - 1))
            ];
        }
      }

      return result;
    };
    return { state, showPassword, changeIsCheck };
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
.bg-main {
  background-color: #15202b;
}
.bg-hot {
  background-color: #ff5311;
}
.bg-sub {
  background-color: #9a9492;
}
.text-hot {
  color: #6ef5d2;
  -webkit-text-stroke-color: white;
  -webkit-text-stroke-width: 0.5px;
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
