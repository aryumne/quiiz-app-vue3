<template>
        <h2 width="100%" class="bg-pink py-3">QUIZ APP</h2>
        <v-progress-linear
          v-model="answeredCounter"
          color="blue-lighten-3"
          height="25"
          striped
        >
          <template v-slot:default="{ value }">
            <strong>{{ Math.ceil(value) }}%</strong>
          </template>
        </v-progress-linear>
        <div
          v-for="(quiz, qi) in questions"
          :key="quiz.q"
          class="pt-4 text-start ps-4"
        >
          <h5 class="mb-2">{{ `${qi + 1}. ${quiz.q}` }}</h5>
          <v-radio-group v-model.prevent="checks[qi]">
            <v-radio
              v-for="(answer, ai) in quiz.options"
              :label="answer.val.toString() + ' = ' + qi"
              :value="answer.val.toString()"
              :key="ai"
            ></v-radio>
          </v-radio-group>
        </div>
</template>

<script>
export default {
  name: "Question",
  props: ["questions", "checks"],
  computed: {
    answeredCounter() {
      let width = 0;
      this.checks.forEach(element => width++)
      return width / this.questions.length * 100
    }
  }
};
</script>
