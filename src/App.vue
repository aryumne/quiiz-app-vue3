<template>
  <v-app>
    <v-main>
      <v-container class="fill-height">
        <v-responsive class="align-center text-center fill-height">
          <v-sheet
            elevation="3"
            rounded
            class="mx-auto fill-height pb-3"
            :max-width="800"
            width="100%"
          >
            <Question v-if="!isSubmitted" :questions="questions" :checks="answereds" />
            <Congratulation v-else="isSubmitted" :score="finalScore" />
            <v-btn
              @click.prevent="resetForm"
              color="warning"
              class="me-2"
            >
              Reset
            </v-btn>
            <v-btn
              @click.prevent="submitForm"
              color="primary"
              :disabled="(questions.length !== answereds.length) || isSubmitted"
            >
              Submit
            </v-btn>
          </v-sheet>
        </v-responsive>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import Question from "@/components/Question.vue";
import Congratulation from "@/components/Congratulation.vue";

export default {
  name: "QuizApp",
  data() {
    return {
      isSubmitted: false,
      finalScore: 0,
      questions: [
        {
          q: "Pemanfaatan barcode scanner diwujudkan dalam bentuk diagram?",
          options: [
            {
              val: "Batang",
              isRight: true,
            },
            {
              val: "Donat",
              isRight: false,
            },
            {
              val: "Biji",
              isRight: false,
            },
          ],
        },
        {
          q: "Beli 2 gratis 1. Kalau saya beli 3, berapa jumlah yang saya dapatkan?",
          options: [
            {
              val: 3,
              isRight: false,
            },
            {
              val: 4,
              isRight: true,
            },
            {
              val: 5,
              isRight: false,
            },
          ],
        },
        {
          q: "Dimana ikan bisa hidup?",
          options: [
            {
              val: "Luar Angkasa",
              isRight: false,
            },
            {
              val: "Air",
              isRight: true,
            },
            {
              val: "Rumah Budi",
              isRight: false,
            },
          ],
        },
        {
          q: "Apa nama profesi yang kerjanya healing di luar angkasa?",
          options: [
            {
              val: "Nelayan",
              isRight: false,
            },
            {
              val: "Kades",
              isRight: false,
            },
            {
              val: "Astronot",
              isRight: true,
            },
          ],
        },
        {
          q: "Berapa hasil dari 3! ?",
          options: [
            {
              val: 20,
              isRight: false,
            },
            {
              val: 6,
              isRight: true,
            },
            {
              val: 10,
              isRight: false,
            },
          ],
        },
      ],
      answereds: [],
    };
  },
  methods: {
    submitForm() {
      let trueAnswers = 0;
      this.isSubmitted = true
      this.answereds.forEach((e, i) => {
        const check = this.questions[i].options.some(ops => ops.val == e && ops.isRight == true)
        console.log(`${e}  is ${check}`)
        if (check) trueAnswers++
      })
      this.finalScore = (trueAnswers / this.questions.length) * 100
    },
    resetForm() {
      this.isSubmitted = false
      this.finalScore = 0
      this.answereds = []
    }
  },
  components: {
    Question,
    Congratulation
  },
};
</script>
