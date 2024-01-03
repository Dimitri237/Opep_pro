<template>
  <div id="app">
    <LoadingPage v-if="showSplashScreen && !hideSplashScreen" />
    <router-view v-else></router-view>
  </div>
</template>

<script>

import LoadingPage from './components/LoadingPage.vue';
export default {
  components: {
    LoadingPage,
  },
  data() {
    return {
      showSplashScreen: true,
      hideSplashScreen: false,
    };
  },
  mounted() {
    // Simulez une attente de quelques secondes avant de masquer le splash screen
    setTimeout(() => {
      this.hideSplashScreen  = true;
    }, 3000);
  },
};
</script>