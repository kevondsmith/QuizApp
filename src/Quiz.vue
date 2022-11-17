<template>
  <div class="mainLayout">
    <QuizCard />
  </div>
</template>

<script>
import QuizCard from "./QuizCard.vue";

export default {
  name: "Quiz",
  components: {
    QuizCard
  }
};
</script>

<style type="text/css" scoped>
.mainLayout {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: rgb(255, 255, 255);
  background-color: #30414E;
  height: 100vh;
  display: flex;
  text-align: center;
  flex-direction: column;
  padding-top: 100px;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-weight: 600;
}
</style>