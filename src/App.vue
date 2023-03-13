<script setup>
import { ref,computed } from 'vue';
import hedear from './components/hedear.vue'
import steper from './components/steper.vue'
const questions =ref([
  {
    question: 'Why is AWS more economical than traditional data centers for applications with varying compute workloads?',
    answer:1,
    options:[
      'Amazon EC2 costs are billed on a monthly basis',
      'Users retain full administrative access to their Amazon EC2 instances',
      'Amazon EC2 instances can be launched on demand when needed.','Users can permanently run enough instances to handle peak workloads.'
    ],
    selected:null
  },
  {
    question: 'Which AWS service would simplify the migration of a database to AWS?',
    answer:1,
    options:[
      'AWS Storage Gateway',
      'AWS Database Migration Service (AWS DMS)',
      'Amazon EC2','Amazon AppStream 2.0'
    ],
    selected:null
  },
  {
    question: 'Which AWS offering enables users to find, buy, and immediately start using software solutions in their AWS environment?',
    answer:1,
    options:[
      'AWS Config',
      'AWS OpsWorks',
      'AWS SDK','AWS Marketplace'
    ],
    selected:null
  },
  {
    question: 'Which AWS networking service enables a company to create a virtual network within AWS?',
    answer:1,
    options:[
      'AWS Config',
      'Amazon Route 53',
      'AWS Direct Connect','Amazon Virtual Private Cloud (Amazon VPC)'
    ],
    selected:null
  },
  {
    question: 'Which of the following is an AWS responsibility under the AWS shared responsibility model?',
    answer:1,
    options:[
      'Configuring third-party applications',
      'Maintaining physical hardware',
      'Securing application access and data','Managing guest operating systems'
    ],
    selected:null
  },
  {
    question: 'Which component of the AWS global infrastructure does Amazon CloudFront use to ensure low-latency delivery?',
    answer:1,
    options:[
      'AWS Regions',
      'Edge locations',
      'Availability Zones',
      'Virtual Private Cloud (VPC)'
    ],
    selected:null
  },
  {
    question: 'How would a system administrator add an additional layer of login security to user\'s AWSManagement Console?',
    answer:1,
    options:[
      'Use Amazon Cloud Directory',
      'Audit AWS Identity and Access Management (IAM) roles',
      'Enable multi-factor authentication',
      'Enable AWS CloudTrail'
    ],
    selected:null
  },
  {
    question: 'Which service can identify the user that made the API call when an Amazon EC2 instance is terminated?',
    answer:1,
    options:[
      'AWS Trusted Advisor',
      'AWS CloudTrail',
      'AWS X-Ray',
      'AWS Identity and Access Management (AWS IAM)'
    ],
    selected:null
  },
  {
    question: 'Which service would be used to send alerts based on Amazon CloudWatch alarms?',
    answer:1,
    options:[
      ' Amazon Simple Notification Service (Amazon SNS)',
      'AWS CloudTrail',
      'AWS Trusted Advisor',
      'Amazon Route 53'
    ],
    selected:null
  },
  {
    question: 'Where can a user find information about prohibited actions on the AWS infrastructure',
    answer:1,
    options:[
      'AWS Trusted Advisor',
      'AWS Identity and Access Management (IAM)',
      'AWS Billing Console',
      'AWS Acceptable Use Policy'
    ],
    selected:null
  }

])
const  quizCompleted=ref(false)
const currentQuestion =ref(0);
//  console.log(questions.value)
const score =computed(()=>{
  return questions.value.filter(q=>q.selected==q.answer).length;
})
const getCurrentQuestion=computed(()=>{
  let question=questions.value[currentQuestion.value]
  return question
})
const SetArnswer= evt =>{
  questions.value[currentQuestion.value].selected=evt.target.value
}
       var active=ref(true).value;
       console.log(active)
      var desactive=ref(false).value;
const NextQuestion =()=>{
  if(currentQuestion.value < questions.value.length-1){
    currentQuestion.value++ 
  }else{
    quizCompleted.value=true;
      active=ref(false).value;
      desactive=ref(true).value
  }
}
</script>
<template>
  <main class="app">
    <hedear calss="logo"></hedear>
    <steper :isactive="active" :active='desactive' ></steper>
    <div class="Container">
      <div>
        <h1>The Quiz</h1>
        <section class="quiz" v-if="!quizCompleted">
          <div class="quiz-info">
            <span class="question">{{ getCurrentQuestion.question }}</span>
            <!-- <span class="score">score {{score}}/{{questions.length}}</span> -->
            <div class="options">
              <label v-for="(option,index) in getCurrentQuestion.options" :key="index"
              :class="`option ${
                getCurrentQuestion.selected == index ? index == getCurrentQuestion.answer ?'correct':'wrong':''}
                ${
                    getCurrentQuestion.selected != null && index !=getCurrentQuestion.selected ? 'disabled' : ''
                }`">
            <input type="radio"
            :name="getCurrentQuestion.index"
            :value="index"
            v-model="getCurrentQuestion.selected"
            :disabled="getCurrentQuestion.selected"
            @change="SetArnswer">
            <span>{{option}}</span>
              </label>
            </div>
          </div>
          <button @click="NextQuestion"
          :disabled="!getCurrentQuestion.selected">
            {{getCurrentQuestion.index==questions.length-1 ? 'finish' :getCurrentQuestion.selected == null ? 'Select an option' :'Next Question'
            }}
          </button>
        </section>
        <section v-else >
          <h2>You have finish the quiz!</h2>
          <p> Your score is {{score}}/{{questions.length}}</p>
        </section>
      </div>
    </div>
  </main>
</template>

<style>
* {
  margin:0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Montserrat',sans-serif;
}
.logo{
  width: 80px;
  height: 70px;
}
.Container{
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 2rem;
  min-height: 80vh;
}
h1{
  font-size: 2rem;
  margin-bottom: 2rem;
}
.quiz{
  background-color: #ebc209;
  padding: 1rem;
  width: 100%;
  max-width: 640px;
}
.quiz-info{
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-bottom:1rem;
}
.quiz-info .question {
  color: #000000;
  font-size :1.25rem;
  margin-bottom:10px ;
}
.options{
  display: flex;
  flex-direction:column ;
  margin-bottom: 0.5rem;
  border-radius:0.5rem;
  cursor:pointer;
}
.option:hover {
  background-color:#e7eb09;
}
.option.correct {
  background-color:rgb(46, 209, 46);
}
.option.wrong{
  background-color: rgb(236, 65, 65);
}
.option.disabled{
  opacity:0.5;
}
.option input {
  display: none;
}
button{
  appearance: none;
  outline: none;
  cursor: pointer;
  padding: 0.5rem 1rem;
  background-color:
  rgb(121, 243, 121);
  color:#3f3e3c;
  font-weight: 700;
  text-transform: uppercase;
  font-size:1.25rem;
  border-radius: 0.5rem;
}
button:disabled{
  opacity: 0.5;
}
h2{
  font-size:2rem;
  margin-bottom: 2rem;
  text-align: center;
}
body {
  background-color: #f1f19c;
  color: rgb(0, 0, 0);
}
</style>
