<template>
  <div>
    <Header />
    <JobsList msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import Header from './components/Header.vue';
import JobsList from './components/JobsList.vue';

export default {
  name: 'App',
  components: {
    Header,
    JobsList,
  }
}
</script>

<style lang="scss">
@import '@/css/reset.scss';
@import '@/css/vars.scss';

body {
  background: $Background;
}

#app {
  min-height: 100vh;
  font-size: $FontSize;
  font-weight: $FontWeight;
  font-family: $FontFamily;
}
</style>
