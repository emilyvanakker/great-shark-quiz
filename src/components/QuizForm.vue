<template>
    <div>
        <h3>Welcome to the Great Shark Quiz</h3>
        <form>
            <div v-if="questionIndex < questions.length">
            <label>{{ question.question }}</label>
            <div v-for="c of question.choices" :key="c">
                <input type="radio" name="choice" v-model="answer" :value="c" />
                {{ c }}
            </div>
            </div>
            <div v-else>
                <button type="button" @click="restart">restart</button>
            </div>
            <button type="button" @click="submit">check</button>
        </form>
        <p>score: {{ score }}</p>
    </div>
</template>

<script>
const questions = [
  {
    question: "Thanks to its kidneys, the _____ shark can survive in fresh water.",
    choices: ["Hammerhead", "Bull", "Tiger", "Great White"],
    rightAnswer: "Bull",
  },
  {
    question: "Tiger sharks can live for up to _____ years.",
    choices: ["25", "50", "60", "75"],
    rightAnswer: "50",
  },
  {
    question: "Approximately how much does a full-grown great white shark weigh?",
    choices: ["1,000 pounds", "2,000 pounds", "3,000 pounds", "5,000 pounds"],
    rightAnswer: "5000",
  },
];
export default {
    name: "QuizForm",
    data() {
        return {
        questions,
        score: 0,
        questionIndex: 0,
        question: questions[0],
        answer: "",
        };
    },
    methods: {
        submit() {
            const { answer, question, questions, questionIndex } = this;
            if (answer === question.rightAnswer) {
                this.score++;
            }
            if (questionIndex < questions.length) {
                this.questionIndex++;
                this.question = { ...questions[this.questionIndex] };
            }
        },
        restart() {
            this.question = questions[0];
            this.answer = "";
            this.questionIndex = 0;
            this.score = 0;
        },
    },
};
</script>

<style>

</style>