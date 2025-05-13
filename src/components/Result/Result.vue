components: { Result, },
<template>
  <div class="resultCard">
    <div>
      <h1>Your Result</h1>
    </div>
    <h3>{{ dataStore.getResult + "/" + dataStore.getTotalQuestion }}</h3>

    <ResultItem
      v-for="(value, index) in dataStore.selectedOptions"
      :options="value"
      :index="index"
      :key="value"
    />

    <button type="button" class="btnHome" @click="emitReset">Home</button>
  </div>
</template>
<script>
import { useDataStore } from "@/store/data";
import { mapStores } from "pinia";
import ResultItem from "./ResultItem.vue";

export default {
  name: "Result",
  components: { ResultItem },
  computed: {
    ...mapStores(useDataStore),
  },
  methods: {
    emitReset() {
      this.$emit("reset");
    },
  },
};
</script>
<style scoped>
.resultCard {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  width: 100%;
  background-color: white;
  border-radius: 10px;
}
.btnHome {
  width: 150px;
  height: 50px;
  background-color: rgb(0, 130, 31);
  color: white;
  margin: 16px;
  font-size: 18px;
  font-weight: bold;
  border: none;
  border-radius: 10px;
}
</style>
