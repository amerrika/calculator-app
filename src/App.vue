<template>
  <ThemeSwitcher />
  <Display :display="display" />
  <div class="buttons-wrapper">
    <Button
      v-for="button in store.buttonsList"
      :key="button.index"
      :button="button"
      @handleClick="calc"
    />
  </div>
</template>

<script>
// import scss-starter
import "./scss/main.scss";
// import components
import Button from "./components/Button.vue";
import Display from "./components/Display.vue";
import ThemeSwitcher from "./components/ThemeSwitcher.vue";
// import store
import { store } from "./store";

export default {
  name: "App",
  components: {
    Button,
    Display,
    ThemeSwitcher,
  },
  data() {
    return {
      store,
      display: "0",
    };
  },
  methods: {
    calc(button) {
      switch (button) {
        case "+":
        case "-":
        case "x":
        case "/":
          if (
            this.display.slice(-1) === "+" ||
            this.display.slice(-1) === "-" ||
            this.display.slice(-1) === "x" ||
            this.display.slice(-1) === "/"
          ) {
            this.display = this.display.slice(0, -1) + button;
          } else {
            this.display += button;
          }
          break;
        case ".":
          if (this.display.slice(-1) === ".") {
            // toast.error("You can't add two decimal points beside")
          } else {
            this.display += button;
          }
          break;
        case "DEL":
          this.display = this.deleteLastChar;
          break;
        case "RESET":
          this.display = "0";
          break;
        case "=":
          if (
            parseInt(this.display.slice(-1)) >= 0 &&
            parseInt(this.display.slice(-1)) <= 9
          ) {
            this.display = this.convertCrossToMultiplication;
            const answer = eval(this.display).toString();
            if (answer === "NaN") {
              this.display = "Undefined";
            } else {
              this.display = answer;
            }
          } else {
            // toast error("Pls add numbers after + - x / ")
          }
          break;
        default:
          if (this.display === "0") {
            this.display = button;
          } else {
            this.display += button;
          }
      }
    },
  },

  computed: {
    deleteLastChar() {
      if (this.display.length === 1) {
        return "0";
      }
      return this.display.slice(0, -1);
    },
    convertCrossToMultiplication() {
      return this.display.replace("x", "*");
    },
  },
};
</script>
