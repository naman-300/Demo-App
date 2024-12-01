<template>
    <div class="question">
      <h3>Q{{ index + 1 }}: {{ question.question }}</h3>
      <div v-for="(option, i) in question.options" :key="i">
        <label>
          <input
            type="radio"
            :name="'q' + index"
            :value="option"
            @change="selectAnswer(option)"
          />
          {{ option }}
        </label>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      question: Object,
      index: Number,
    },
    methods: {
      selectAnswer(answer) {
        this.$emit('answer', { index: this.index, answer });
      },
    },
  };
  </script>
  
  <style>
  .question {
    margin: 15px 0;
  }
  </style>
  