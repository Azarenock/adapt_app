<template>
<div>
  <div v-if="loaded">
    <h3>{{  topics[selectedTopic].topicName }}</h3>
    <p> {{  topics[selectedTopic].questions[selectedQuestion].title }}</p>
    User selected: {{ userSelectAnswer }} / Score: {{  score }}
    
    <div v-for="opt in topics[selectedTopic].questions[selectedQuestion].options" :key="opt">
      <input type="radio" :value="opt" v-model="userSelectAnswer" />
      <label>{{  opt }}</label>
    </div>
    <button @click="checkUser">check answer</button>
  </div>
</div>
</template>

<script>


export default {
  name: 'App',
  data() {
    return {
      selectedTopic: 0,
      selectedQuestion: 0,
      userSelectAnswer: 0,
      score: 0,
      loaded: false,
      topics: [
    {
        "topicName": "Topic #1",
        "canGoTo": [
            2,
            3
        ],
        "hint1": "Text hint 1",
        "hint2": "Text hint 2",
        "hint3": "/image_1.png",
        "questions": [
            {
                "title": "What is 2+2?",
                "diff": 0,
                "options" :[3, 5, 7, 4],
                "answer": 4
            },
            {
                "title": "What is 3+7?",
                "diff": 0,
                "options": [10, 5, 3, 11],
                "answer": 10
            },
            {
                "title": "What is 1+3?",
                "diff": 1,
                "options":[4, 6, 90, 3],
                "answer": 4
            },
            {
                "title": "What is 6+1?",
                "diff": 1,
                "options":[7, 5, 80, 3],
                "answer": 7
            }
        ]
    }
]
    }
  },
  methods: {
    checkUser() {
      if(this.userSelectAnswer == this.topics[this.selectedTopic].questions[this.selectedQuestion].answer) {
        this.score += 1;
      }
      else {
        this.score -= 0.25;
      }
      if(this.score <= -0.75) {
        //tell user to READ THEORY
      }
      if(this.score >= 1) {
        //select another topic
      }
    }
  },
  components: {
    
  },
  mounted() {

    this.loaded = true;
  }
}
</script>

<style>

</style>
