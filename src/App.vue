<template>
  <div id="app">
    <Header />
    <div class="container">
      <QuestionBox
        v-if="questions.length > 0"
        :nextQuestion="nextQuestion"
        :questionData="questions[index]"
      />
      <p v-else>
        Loading...
      </p>
    </div>
  </div>
</template>

<script>
import Header from "@/components/Header.vue";
import QuestionBox from "@/components/QuestionBox.vue";

export default {
  name: "Home",
  components: {
    Header,
    QuestionBox
  },
  data() {
    return {
      loading: true,
      questions: [],
      index: 0
    };
  },
  methods: {
    nextQuestion() {
      if (this.index < this.questions.length - 1) {
        this.index++;
      }
    }
  },
  mounted() {
    fetch("https://opentdb.com/api.php?amount=10&category=21&type=multiple", {
      method: "GET"
    })
      .then(res => {
        return res.json();
      })
      .then(data => {
        this.questions = data.results;
      });
  }
};
</script>

<style lang="scss"></style>
