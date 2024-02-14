<template>
  <button class="btn" :class="buttonType" @click="handleClick">
    {{ button.data }}
  </button>
</template>

<script>
export default {
  props: {
    button: Object,
  },
  methods: {
    handleClick() {
      this.$emit("handleClick", this.button.data);
    },
  },
  computed: {
    buttonType() {
      // returns css class
      return this.button.data === "RESET"
        ? "btn-reset"
        : this.button.data === "DEL"
        ? "btn-del"
        : this.button.data === "="
        ? "btn-equal"
        : "";
    },
  },
};
</script>
