<template>
  <div class="header">
    <div class="logo">
      <p>calc</p>
    </div>
    <div class="switcher-wrapper">
      <div class="empty"></div>
      <div>
        <span v-for="theme in themes">{{ theme.name }}</span>
      </div>
      <div>
        <p>THEME</p>
      </div>
      <div>
        <button
          class="button-theme"
          v-for="theme in themes"
          :class="{ active: theme.name === this.currentTheme }"
          @click="changeCurrentTheme(theme.name)"
        ></button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      themes: [
        {
          name: "1",
          current: true,
        },
        {
          name: "2",
          current: false,
        },
        {
          name: "3",
          current: false,
        },
      ],
      currentTheme: "1",
    };
  },
  methods: {
    applyCurrentTheme(theme) {
      document.documentElement.setAttribute("data-theme", theme);
    },
    changeCurrentTheme(theme) {
      this.currentTheme = theme;
    },
  },
  watch: {
    currentTheme(newTheme) {
      this.applyCurrentTheme(newTheme);
    },
  },
};
</script>
