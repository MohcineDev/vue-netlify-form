<template>
  <div class="home">
    <Contact />
  </div>
</template>

<script>
// @ is an alias to /src
import Contact from "@/components/Contact.vue";

export default {
  name: "Home",
  components: {
    Contact,
  },
};
</script>

<style scoped>
</style>