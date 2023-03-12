<script setup>
import { ref,computed } from 'vue';
const questions =ref([
  {
    question: 'Why is AWS more economical than traditional data centers for applications with varying compute workloads?',
    answer:0,
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
    answer:2,
    options:[
      'AWS Config',
      'AWS OpsWorks',
      'AWS SDK','AWS Marketplace'
    ],
    selected:null
  },
  {
    question: 'Which AWS networking service enables a company to create a virtual network within AWS?',
    answer:3,
    options:[
      'AWS Config',
      'Amazon Route 53',
      'AWS Direct Connect','Amazon Virtual Private Cloud (Amazon VPC)'
    ],
    selected:null
  },
  {
    question: 'Which of the following is an AWS responsibility under the AWS shared responsibility model?',
    answer:4,
    options:[
      'Configuring third-party applications',
      'Maintaining physical hardware',
      'Securing application access and data','Managing guest operating systems'
    ],
    selected:null
  },
  {
    question: 'Which component of the AWS global infrastructure does Amazon CloudFront use to ensure low-latency delivery?',
    answer:5,
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
    answer:6,
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
    answer:7,
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
    answer:8,
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
    answer:9,
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
const currentQuestion =ref(0)
const score =computed(()=>{
  let value =0
  questions.value.map(q=>{
    if(q.selected==q.answer){
      value++
    }
  })
  return value
})
const getCurrentQuestion=computed(()=>{
  let question=questions.value[currentQuestion.value]
  question.index =currentQuestion.value
  return question
})
const SetArnswer= evt =>{
  questions.value[currentQuestion.value].selected=evt.target.value
  evt.target.value=null
}
const NextQuestion =()=>{
  currentQuestion.value++
  if(currentQuestion.value < questions.value.length-1){
    currentQuestion.value++
  }else{
    quizCompleted.value=true
  }
}
</script>

<template>
  <main class="app">
    <h1>The Quiz</h1>
    <section class="quiz">
      <div class="quiz-info">
        <span class="question">{{ getCurrentQuestion }}</span>
        <span class="score">score {{score}}/{{questions.length}}</span>
        <div class="options"></div>
      </div>
    </section>
  </main>
</template>

<style>
* {
  margin:0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Montserrat',sans-serif;
}
body {
  background-color: #271C36;
  color: white;
}
</style>
