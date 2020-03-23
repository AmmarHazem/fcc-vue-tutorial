<template>
  <div class="jumbotron">
    <p class="lead">
      {{ questionData.question }}
    </p>
    <hr class="my-4" />
    <div v-for="(a, index) in answers" :key="index" class="list-group">
      <button
        @click="selectAnswer(index)"
        type="button"
        :class="{ active: selectedAnswer === index }"
        class="list-group-item list-group-item-action mb-2"
      >
        {{ a }}
      </button>
    </div>
    <button class="btn btn-primary">Submit</button>
    <span class="mx-2"></span>
    <button class="btn btn-success" @click="nextQuestion">Next</button>
  </div>
</template>

<script>
export default {
  props: {
    questionData: {
      type: Object,
      default: function() {
        return {};
      }
    },
    nextQuestion: {
      type: Function
    }
  },
  data() {
    return {
      selectedAnswer: null
    };
  },
  methods: {
    selectAnswer(index) {
      this.selectedAnswer = index;
    }
    // shuffleAnswers() {
    //   let answers = [
    //     ...this.questionData.incorrect_answers,
    //     this.questionData.correct_answer
    //   ];
    // }
  },
  watch: {},
  computed: {
    answers() {
      let answers = [...this.questionData.incorrect_answers];
      answers.push(this.questionData.correct_answer);
      return answers;
    }
  }
};
</script>
