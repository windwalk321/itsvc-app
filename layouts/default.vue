<template>
  <div class="default-layout">
    <Nuxt />
  </div>
</template>

<style>
html {
  font-family:
    'Source Sans Pro',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
  margin-left: calc(100vw - 100%);
  margin-right: 0;
}

body {
  background: rgb(36, 40, 47);
}

*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
}
.default-layout {
  min-height: 100vh;
  max-width: 1200px;
  margin: 0 auto;
  padding: 1rem;
}
</style>
