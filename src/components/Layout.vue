<template>
  <div v-if="!showResult" class="mainBox">
    <Timer v-if="startQuiz" :timer="timer" />

    <div class="QuizList" v-if="!startQuiz">
      <QuizList
        v-for="(tittle, index) in dataStore.getAllQuizes"
        :tittle="tittle"
        :index="index"
        :key="tittle"
        @start="setTimerStart"
      />
    </div>

    <div v-if="startQuiz" class="QuizBox">
      <QuizBox @showResult="showResult = true" />
    </div>
  </div>

  <div v-if="showResult" class="Result">
    <Result @reset="reset" />
  </div>
</template>
<script>
import { mapStores } from "pinia";
import { useDataStore } from "@/store/data";
import QuizList from "@/components/QuizList.vue";
import QuizBox from "./QuizBox.vue";
import Result from "@/components/Result/Result.vue";
import Timer from "@/components/Timer.vue";

export default {
  name: "Layout",
  components: { QuizList, QuizBox, Result, Timer },
  data() {
    return {
      startQuiz: false,
      showResult: false,
      timer: 10,
    };
  },
  computed: {
    ...mapStores(useDataStore),
  },
  methods: {
    reset() {
      this.startQuiz = false;
      this.showResult = false;
      this.timer = 10;
      this.dataStore.reset();
    },
    setTimerStart() {
      this.startQuiz = true;
      console.log("object");
      const intervalid = setInterval(() => {
        if (this.timer <= 0) {
          clearInterval(intervalid);
          this.timer = 0;
          let empty = false;
          if (this.dataStore.selectedOptions.length === 0) {
            empty = true;
          }
          for (
            let i = this.dataStore.selectedOptions.length;
            i < this.dataStore.getTotalQuestion;
            i++
          ) {
            if (!empty) {
              this.dataStore.setNextQuestion();
            }
            this.dataStore.setSelectedOptions("");
            empty = false;
          }
          this.showResult = true;
        }
        this.timer -= 1;
      }, 1000);
    },
  },
};
</script>
<style scoped>
.mainBox {
  display: flex;
  flex-direction: column;
  height: 100vh;
  justify-content: center;
  align-items: center;
  background-color: transparent;
}
.QuizList {
  width: 100%;
}
.QuizBox {
  width: 100%;
}
.Result {
  width: 100%;
}
</style>
