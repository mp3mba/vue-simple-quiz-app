<template>
    <div class="container">
      <div class="box">
        <h2>{{ question }}</h2>
        <div v-for="(answer, index) in answers" :key="index">
          <input type="radio" :value="answer" v-model="selectedAnswer" @change="checkAnswer">
          {{ answer }}
        </div>
        <button v-if="isQuizFinished" @click="startQuiz">Start Again</button>
        <div v-else>
          <button @click="nextQuestion" :disabled="!selectedAnswer">Next Question</button>
        </div>
      </div>
      <div class="score">
        <h3>Your score: {{ score }}/{{ totalQuestions }}</h3>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'quizPage',
    data(){
        return{
            questions: [
                {
                question: 'What is the capital of France?',
                answers: ['Paris', 'London', 'Berlin', 'Madrid'],
                correctAnswer: 'Paris'
                },
                {
                question: 'What is the capital of Tanzania?',
                answers: ['Nairobi', 'Bujumbura', 'Kampala', 'Dodoma'],
                correctAnswer: 'Dodoma'
                },
                {
                question: ' Which planet is closest to the Sun?',
                answers: ['Mercury', 'Earth', 'Neptune', 'Uranus'],
                correctAnswer: 'Mercury'
                },
                {
                question: 'What is the largest planet in our solar system?',
                answers: ['Jupiter', 'Saturn', 'Neptune', 'Uranus'],
                correctAnswer: 'Jupiter'
                },
                {
                question: 'Who was the first person to step on the moon?',
                answers: ['Neil Armstrong', 'Buzz Aldrin', 'Michael Collins', 'Yuri Gagarin'],
                correctAnswer: 'Neil Armstrong'
                }
            ],
            selectedAnswer: '',
            currentQuestionIndex: 0,
            score: 0
        }
    },
    computed: {
      question() {
        return this.questions[this.currentQuestionIndex].question;
      },
      answers() {
        return this.questions[this.currentQuestionIndex].answers;
      },
      totalQuestions() {
        return this.questions.length;
      },
      isQuizFinished() {
        return this.currentQuestionIndex === this.totalQuestions-1;
      }
    },
    methods: {
      checkAnswer() {
        const correctAnswer = this.questions[this.currentQuestionIndex].correctAnswer;
        if (this.selectedAnswer === correctAnswer) {
          this.score++;
        }
        console.log(this.currentQuestionIndex)
      },
      nextQuestion() {
        this.selectedAnswer = '';
        this.currentQuestionIndex++;
        if(this.currentQuestionIndex == this.currentQuestionIndex-1){
          return
        }
      },
      startQuiz() {
        this.selectedAnswer = '';
        this.currentQuestionIndex = 0;
        this.score = 0;
      }
    },
  }
  </script>

<style scoped>
.container{
  background-image: linear-gradient(15deg, #ffae00 , #934f02);
  padding: 9px;
  border-radius: 7px;
  color: white;
  display: flex;
  justify-content: space-around;
}
.box{
  margin-top: 0;
  text-align: left;
}
input{
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  border: 2px solid #ccc;
  outline: none;
  cursor: pointer;
}
input:checked{
  background-color: #ffffff;
  border-color: #f3f3f3;
}
button{
  padding: 7px;
  background-color: rgb(194, 12, 194);
  border: none;
  cursor: pointer;
  border-radius: 5px;
  margin-top: 10px;
  color: white;
  font-weight: 900;
  transition: background-color .9s;
}
button:hover{
  background-color: purple;
  transition: background-color .9s;
}

.score{
  background-color: rgb(40, 231, 40);
  height: 30px;
  display: flex;
  justify-content: center;
  align-items: center;
  color: rgb(38, 37, 37);
  padding: 6px;
  border-radius: 7px;
}
</style>