<template>
  <div class="container">
    <img
      src="@/assets/images/cookie.png"
      class="right m-2"
      @click="toggleSidepanel"
    />
    <Sidepanel v-if="showSidepanel" class="side" />
    <Nuxt />
  </div>
</template>

<script>
export default {
  data() {
    return {
      showSidepanel: false,
    }
  },
  methods: {
    toggleSidepanel() {
      this.showSidepanel = !this.showSidepanel
    },
  },
}
</script>

<style>
.container {
  position: relative;
}

img {
  height: 6em;
  cursor: pointer;
  position: fixed;
  bottom: 0;
  right: 0;
}
</style>
