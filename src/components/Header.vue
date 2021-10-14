<template>
  <header class="header">
  </header>
</template>

<script>
export default {
  name: 'Header',
}
</script>

<style scoped lang="scss">
@import '@/css/vars.scss';

.header {
  background: url('../assets/images/bg-header-desktop.svg');  
  height: 8rem;
}

/* Small screen */
@media only screen and (max-width: 1440px) {
  .header {
    background: url('../assets/images/bg-header-mobile.svg');  
    height: 8rem;
  }
}
</style>
