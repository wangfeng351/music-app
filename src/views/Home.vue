<template>
  <div class="home">
    <SingerVue msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script>
// @ is an alias to /src
// eslint-disable-next-line no-unused-vars
import SingerVue from "@/components/singer.vue";

export default {
  name: "Home",
  components: {
    SingerVue
  }
};
</script>
