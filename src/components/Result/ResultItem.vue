<template>
  <div :class="options.result ? 'right box' : 'wrong box'">
    <h1>{{ dataStore.getCustomQuestion(index) }}</h1>
    <p>
      Correct Answer: <span>{{ options.answer }}</span>
    </p>
    <p>
      Your Answer: <span>{{ options.selected }}</span>
    </p>
  </div>
</template>
<script>
import { useDataStore } from "@/store/data";
import { mapStores } from "pinia";

export default {
  props: ["options", "index"],
  computed: {
    ...mapStores(useDataStore),
  },
};
</script>
<style>
.right {
  color: green;
  border-color: green;
}
.wrong {
  color: red;
  border-color: red;
}
.box {
  width: 80%;
  height: 90%;
  margin: 16px;
  border: 2px;
  border-style: solid;
  border-radius: 10px;
  padding: 16px;
}
</style>
