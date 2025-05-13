<template>
  <div class="mainBg">
    <layout />
  </div>
</template>

<script>
import Layout from "./components/Layout.vue";
export default {
  components: { Layout },
};
</script>
<style scoped>
.mainBg {
  background-image: url("https://templates.seekviral.com/qzain/quiz/Quiz10/assets/images/bg.png");
  background-position: 50% 50%;
  /* background-size: cover; */
  width: 100%;
  min-height: 100vh;
}
</style>
