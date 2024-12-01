<template>
    <div class="quiz-container">
      <div class="header">
        <h1>Professional Quiz App</h1>
        <div class="timer">Time Left: {{ time }}s</div>
      </div>
      <div class="questions">
        <Question
          v-for="(q, index) in shuffledQuestions"
          :key="q.id"
          :question="q"
          :index="index"
          @answer="handleAnswer"
        />
      </div>
      <div class="actions">
        <button class="submit-btn" @click="calculateScore">Submit</button>
        <button class="reset-btn" @click="resetQuiz">Reset</button>
      </div>
      <div v-if="score !== null" class="score">
        <p>Your Score: <span>{{ score }}</span></p>
      </div>
    </div>
  </template>
  
  <script>
  import Question from './Question.vue';
  
  export default {
    components: {
      Question,
    },
    data() {
      return {
        time: 60,
        score: null,
        answers: [],
        shuffledQuestions: [],
        questions: [
          { id: 1, question: 'What is the capital of France?', options: ['Paris', 'Berlin', 'Madrid', 'Rome'], answer: 'Paris' },
          { id: 2, question: 'Which is the largest planet in our solar system?', options: ['Earth', 'Jupiter', 'Saturn', 'Mars'], answer: 'Jupiter' },
          { id: 3, question: 'What is the speed of light?', options: ['300,000 km/s', '150,000 km/s', '500,000 km/s', '1,000 km/s'], answer: '300,000 km/s' },
          { id: 4, question: 'Who wrote "Hamlet"?', options: ['Shakespeare', 'Dickens', 'Hemingway', 'Tolkien'], answer: 'Shakespeare' },
          { id: 5, question: 'Which element has the chemical symbol O?', options: ['Oxygen', 'Gold', 'Silver', 'Iron'], answer: 'Oxygen' },
          { id: 6, question: 'How many continents are there?', options: ['5', '6', '7', '8'], answer: '7' },
          { id: 7, question: 'What is the square root of 64?', options: ['6', '7', '8', '9'], answer: '8' },
          { id: 8, question: 'Which is the longest river in the world?', options: ['Amazon', 'Nile', 'Yangtze', 'Mississippi'], answer: 'Nile' },
          { id: 9, question: 'Who painted the Mona Lisa?', options: ['Van Gogh', 'Da Vinci', 'Picasso', 'Monet'], answer: 'Da Vinci' },
          { id: 10, question: 'What is the capital of Canada?', options: ['Ottawa', 'Toronto', 'Vancouver', 'Montreal'], answer: 'Ottawa' },
          { id: 11, question: 'What is the freezing point of water?', options: ['0°C', '32°C', '100°C', '-10°C'], answer: '0°C' },
          { id: 12, question: 'Which gas do plants absorb?', options: ['Oxygen', 'Carbon Dioxide', 'Nitrogen', 'Hydrogen'], answer: 'Carbon Dioxide' },
          { id: 13, question: 'What is 5 + 3 x 2?', options: ['11', '13', '16', '21'], answer: '11' },
          { id: 14, question: 'What is the capital of Japan?', options: ['Kyoto', 'Osaka', 'Tokyo', 'Hiroshima'], answer: 'Tokyo' },
          { id: 15, question: 'Which planet is known as the Red Planet?', options: ['Earth', 'Mars', 'Venus', 'Jupiter'], answer: 'Mars' },
          { id: 16, question: 'What is the chemical formula for water?', options: ['H2O', 'CO2', 'NaCl', 'O2'], answer: 'H2O' },
          { id: 17, question: 'Who discovered gravity?', options: ['Newton', 'Einstein', 'Tesla', 'Galileo'], answer: 'Newton' },
          { id: 18, question: 'What is the capital of Italy?', options: ['Venice', 'Rome', 'Florence', 'Naples'], answer: 'Rome' },
          { id: 19, question: 'What is the smallest prime number?', options: ['0', '1', '2', '3'], answer: '2' },
          { id: 20, question: 'What is the largest ocean?', options: ['Atlantic', 'Indian', 'Arctic', 'Pacific'], answer: 'Pacific' },
        ],
      };
    },
    methods: {
      shuffleQuestions() {
        this.shuffledQuestions = this.questions.sort(() => 0.5 - Math.random()).slice(0, 5);
      },
      handleAnswer({ index, answer }) {
        this.answers[index] = answer;
      },
      calculateScore() {
        let score = 0;
        this.shuffledQuestions.forEach((q, i) => {
          if (q.answer === this.answers[i]) {
            score++;
          }
        });
        this.score = score;
      },
      resetQuiz() {
        this.score = null;
        this.answers = [];
        this.time = 60;
        this.shuffleQuestions();
        this.startTimer();
      },
      startTimer() {
        const timer = setInterval(() => {
          if (this.time <= 1) {
            clearInterval(timer);
            this.time = 0;
          } else {
            this.time--;
          }
        }, 1000);
      },
    },
    mounted() {
      this.shuffleQuestions();
      this.startTimer();
    },
  };
  </script>
  
  <style>
  .quiz-container {
  max-width: 700px;
  margin: 10px;
  border-radius: 15px;
  background: rgba(255, 255, 255, 0.1);
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.2);
  backdrop-filter: blur(10px);
  text-align: center;
  color: #ffffff;
  font-family: 'Roboto', sans-serif;
}

.header {
  margin-bottom: 20px;
}

h1 {
  font-size: 2.5rem;
  font-weight: 700;
  background: linear-gradient(90deg, #ff7eb3, #ff758c);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  margin-bottom: 10px;
}

.timer {
  font-size: 1.5rem;
  font-weight: bold;
  color: #ff5722;
  background: rgba(0, 0, 0, 0.2);
  padding: 10px 20px;
  border-radius: 25px;
  display: inline-block;
}

.questions {
  margin: 20px 0;
}

.actions {
  display: flex;
  justify-content: center;
  gap: 20px;
  margin-top: 20px;
}

.submit-btn,
.reset-btn {
  background: linear-gradient(90deg, #36d1dc, #5b86e5);
  color: #fff;
  padding: 10px 25px;
  border: none;
  border-radius: 25px;
  font-size: 16px;
  font-weight: bold;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
}

.submit-btn:hover,
.reset-btn:hover {
  transform: translateY(-3px);
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.3);
}

.reset-btn {
  background: linear-gradient(90deg, #f5576c, #f093fb);
}

.score {
  margin-top: 30px;
  font-size: 1.5rem;
  font-weight: bold;
  color: #4caf50;
  background: rgba(0, 0, 0, 0.2);
  padding: 15px;
  border-radius: 15px;
  display: inline-block;
}

body {
  background: linear-gradient(120deg, #36d1dc, #ff7eb3);
  height: 100vh;
  margin: 0;
  display: flex;
  align-items: center;
  justify-content: center;
}

  .actions {
    display: flex;
    justify-content: center;
    gap: 10px;
  }
  
  .reset-btn {
    background-color: #f44336;
    color: white;
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-size: 16px;
  }
  
  .reset-btn:hover {
    background-color: #d32f2f;
  }
  </style>
  