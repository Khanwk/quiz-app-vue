<template>
  <div class="QuizBox">
    <div class="progressBg"><div class="progressFill"></div></div>

    <div class="QuizBg">
      <div>
        <h1>{{ dataStore.getCurrentQuestion.question }}</h1>

        <Options
          v-for="(item, index) in dataStore.getCurrentQuestion.options"
          :key="index"
          :option="item"
          :index="index"
          @selected="setSelectedOption"
        />
      </div>
      <img
        src="https://templates.seekviral.com/qzain/quiz/Quiz10/assets/images/Manthinking-bro.png"
      />
    </div>
    <button
      v-if="!dataStore.getIsLastQuestion"
      type="button"
      class="nextButton"
      @click="nextQuestion"
    >
      Next Question
    </button>

    <button
      v-if="dataStore.getIsLastQuestion"
      type="button"
      class="nextButton"
      @click="emitDone"
    >
      Done
    </button>
  </div>
</template>
<script>
import { useDataStore } from "@/store/data";
import { mapStores } from "pinia";
import Options from "./Options.vue";

export default {
  components: { Options },
  data() {
    return {
      totalQuestion: 0,
      curentQuestion: 1,
      selectedOption: "",
    };
  },
  computed: {
    ...mapStores(useDataStore),
  },
  watch: {
    "dataStore.currentQuestion": {
      handler: function () {
        console.log("object");
        this.curentQuestion = this.dataStore.getQuestionIndex + 1;
      },
    },
  },
  methods: {
    setSelectedOption(option) {
      this.selectedOption = option;
      this.dataStore.setSelectedOptions(option);
    },
    nextQuestion() {
      if (this.selectedOption !== "") {
        this.dataStore.setNextQuestion();
        this.selectedOption = "";
      }
    },
    emitDone() {
      this.$emit("showResult");
    },
  },
  onMounted() {
    this.totalQuestion = this.dataStore.getTotalQuestion;
  },
};
</script>
<style>
.QuizBox {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 80%;
  height: auto;
  background-color: white;
}
.progressBg {
  background-color: rgb(204, 204, 204);
  width: 80%;
  height: 25px;
  display: flex;
}
.progressFill {
  background-color: rgb(0, 130, 31);
  width: calc((100% / v-bind(totalQuestion)) * ((v-bind(curentQuestion))));
  height: 25px;
}

.QuizBg {
  display: flex;
  width: 100%;
  flex-direction: row;
  justify-content: space-around;
  padding: 16px;
}
.nextButton {
  background-color: rgb(0, 130, 31);
  color: white;
  height: 50px;
  font-size: 18px;
  width: 150px;
  border: none;
  border-radius: 10px;
}
.nextButton:disabled {
  background-color: rgb(204, 204, 204);

  height: 50px;
  font-size: 18px;
  width: 150px;
  border: none;
  border-radius: 10px;
}
</style>
