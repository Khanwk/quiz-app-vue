<template>
  <div class="Bg">
    <button type="button" class="listItem" :onclick="startQuiz">
      {{ tittle }}
    </button>
  </div>
</template>
<script>
import { useDataStore } from "@/store/data";
import { mapStores } from "pinia";

export default {
  name: "QuizList",
  props: ["tittle", "index"],
  computed: {
    ...mapStores(useDataStore),
  },
  methods: {
    startQuiz() {
      this.dataStore.setCurrentQuiz(this.index);
      this.$emit("start");
    },
  },
};
</script>
<style scoped>
.Bg {
  width: 100%;
  display: flex;
  justify-content: center;
  align-content: center;
}
.listItem {
  width: 20%;
  height: 100px;
  border-radius: 10px;
  background-color: rgb(222, 247, 229);
  font-size: 22px;
  font-weight: bold;
  font-family: "Jost";
  margin: 16px;
}
</style>
