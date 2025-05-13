<template>
  <div class="mianOptionDiv" @click="emitOption">
    <div
      :class="
        option === dataStore.getSelected
          ? 'optionNoSelected optionMainNo'
          : 'optionNo optionMainNo'
      "
    >
      <h1>{{ optionNo[index] }}</h1>
    </div>
    <div
      :class="
        option === dataStore.getSelected
          ? 'optionNoSelected optionTittleMain'
          : 'optionNo optionTittleMain'
      "
    >
      <h1>{{ option }}</h1>
    </div>
  </div>
</template>
<script>
import { useDataStore } from "@/store/data";
import { mapStores } from "pinia";

export default {
  props: ["option", "index"],
  data() {
    return {
      optionNo: ["A", "B", "C", "D"],
    };
  },
  computed: {
    ...mapStores(useDataStore),
  },
  methods: {
    emitOption() {
      this.$emit("selected", this.option);
    },
  },
};
</script>
<style scoped>
.mianOptionDiv {
  display: flex;
  flex-direction: row;
  height: 100px;
  width: 400px;
  margin-top: 16px;
  cursor: pointer;
}
.optionMainNo {
  width: 70px;
  height: 100px;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 10px;
}
.optionNo {
  background-color: rgb(204, 204, 204);
}
.optionNoSelected {
  background-color: rgb(0, 130, 31);
  color: white;
}
.optionTittleMain {
  width: 300px;
  height: 100px;
  margin-left: 10px;
  padding-left: 16px;
  display: flex;
  justify-content: start;
  align-items: center;
  border-radius: 10px;
}
</style>
