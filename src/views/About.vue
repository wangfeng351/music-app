<template>
  <div class="about">
    <SongVue msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script>
// @ is an alias to /src
// eslint-disable-next-line no-unused-vars
import SongVue from "@/components/song.vue";

export default {
  name: "About",
  components: {
    SongVue
  }
};
</script>
