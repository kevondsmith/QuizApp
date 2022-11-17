<template>
  <div class="mainCard">
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />

    <!-- intro screen to quiz -->
    <div class="introScreen" v-if="!quizStarted">
        <div class="introCard">
          <div class="titleImage">
            <img
              src="./assets/logo.png"
              alt="image"
              img-top
              title="Quiz App"
              style="max-width: 32rem"
            />
          </div>
          <p>
            <br />
            Simple Quiz
            <br />
          </p>
          <button class="btn" @click="startQuiz()" type="button">
            Start Quiz
          </button>
        </div>
    </div>

      <!-- questions screen  -->
        <div class="QuestionsScreen" v-if="quizStarted">
          <div class="qnaCard" v-if="currentQuestion < questions.length">
            <div class="titleImageQuestions">
              <img
                src="./assets/logo.png"
                alt="image"
                img-top
                title="Quiz App"
                style="max-width: 32rem"
              />
            </div>
            <br />
            <h3>
              {{ questions[currentQuestion].text }}
            </h3>
            <br />

            <div
              v-for="(answers, index) in questions[currentQuestion].answers"
              :key="index"
              class="radio-btn-card"
            >
             <input
                :name="'Question '+currentQuestion"  
                :id="'Answer '+index"
                :value="answers" 
                type="radio"
                v-model="selectedAnswers[currentQuestion]"
            />
            <label :for="'Answer '+index"> 
              <span>
              {{ answers }} 
              </span>
            </label>
            </div>
            <button 
                class="nextbtn"
                @click="nextQuestion()" 
                type="button"
                :disabled="selectedAnswers[currentQuestion] == null || currentQuestion >= questions.length"
            >
              {{ currentQuestion == questions.length - 1 ? 'Submit' : 'Next' }}
            </button>
          </div>

      <!-- summary screen for quiz  -->
        <div class="summaryCard" v-else>
          <div class="titleImage">
            <img
              src="./assets/logo.png"
              alt="image"
              img-top
              title="Quiz App"
              style="max-width: 32rem"
            />
          </div>

          <div class="summarySecondaryCard">
            <h1>Summary</h1>
            <br />
            <hr class="solid" />
            <br />
            <div
              class="quizSummary"
              v-for="(questions, index) in questions"
              :key="index"
            >
                <p>
                  <ul class="answers">
                  <li>{{ questions.text }}</li>
                  <li>{{ selectedAnswers[index] }}</li>
                  </ul>
                </p>
            </div>
          </div>
          <br />
          <button class="btn" @click="restartQuiz($event)" type="button">
            Restart Quiz
          </button>
        </div>
        </div>
    </div>
</template>

<script>
import questions from "@/questions.js";

export default {
  name: "Quiz",
  data() {
    return {
      quizStarted: false,
      questions,
      currentQuestion: 0,
      selectedAnswers: [],
      isSummary: false,
      summary: []
    };
  },
  methods: {
    startQuiz() {
      this.quizStarted = true;
    },

    nextQuestion() {
      this.currentQuestion += 1;
    },

    restartQuiz() {
      this.currentQuestion = 0;
      this.selectedAnswers = Array(this.questions.length).fill(null);
      this.isSummary = false;
      this.quizStarted = false;
    }
  }
};
</script>


<style type="text/css" scoped>
html {
  line-height: 3;
}
</style>