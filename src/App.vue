<template>
  <div id="app">
    <main>
      <component :is="currentView" />
    </main>
    <MainFooter />
  </div>
</template>

<script>
import ProductCatalog from './components/ProductCatalog.vue'
import PrivacyPolicy from './components/PrivacyPolicy.vue'
import MainFooter from './components/MainFooter.vue'
import { ref, computed, onMounted, onUnmounted } from 'vue'

export default {
  name: 'App',
  components: {
    ProductCatalog,
    PrivacyPolicy,
    MainFooter
  },
  setup() {
    const currentPath = ref(window.location.hash)

    onMounted(() => {
      window.addEventListener('hashchange', () => {
        currentPath.value = window.location.hash
      })
    })

    const currentView = computed(() => {
      if (currentPath.value === '#/privacy') {
        return PrivacyPolicy
      }
      return ProductCatalog
    })

    return {
      currentView
    }
  }
}
</script>

<style>
body {
  margin: 0;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
}

#app {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

main {
  flex: 1;
}
</style>