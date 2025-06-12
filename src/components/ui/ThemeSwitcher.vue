<template>
  <button class="theme-switcher gray-bg" aria-label="Light theme only" type="button" disabled>
    <LampOnSVG class="animated on" />
  </button>
</template>

<script setup>
// 僅保留 light，不需切換
</script>

<style scoped>
.theme-switcher {
  background: transparent;
  outline: 0;
  cursor: default;
  & svg {
    position: absolute;
    transform: scale(0.9);
    right: 0;
    top: -115%;
  }
  &:focus-visible svg {
    outline: 2px dashed var(--color-primary);
  }
}
.gray-bg {
  background: #f3f3f3 !important;
}
</style>