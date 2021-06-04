### Description

You will be creating a REST API that works with a “data” source of questions and answers. You will create all of the code to work with the data source using a code module, and test the code module code using provided testing code. You will also create a Node.js REST API to handle the GET verb.

### Code

**p4-data.js**

// Question and answer data array
const data = [
    {
      question: "Q1",
      answer: "A1",
    },
    {
      question: "Q2",
      answer: "A2",
    },
    {
      question: "Q3",
      answer: "A3",
    },
  ];
  
  // Export statement must be below data declaration - no hoisting with const
  module.exports = {
    data,
  };
  
  **p4-module.js**
  
  const fs = require("fs")
const fastify = require("fastify")();
const { data } = require("./p4-data.js");

function getQuestions(){
    const newArray = [];
    for (const obj of data) {
        newArray.push(obj.question);
    }
    return newArray;
}

function getAnswers(){
    const newArray = [];
    for (const obj of data) {
        newArray.push(obj.answer);
    }
    return newArray;
}

function getQuestionsAnswers(){
    const newArray = [];
    for (const obj of data) {
        newArray.push(obj);
    }
    return newArray;
}

function getQuestion(number = "") {
    const specificQuestion = {error: "", question: "", number: ""
    }
    if(!Number.isInteger(number)){
        specificQuestion.error = 'Question number needs to be an integer'
    }
    else if(number > 3){
        specificQuestion.error = 'Question number needs to be less than the number of questions (3)'
    }
    else if(number < 1){
        specificQuestion.error = 'Question number must be greater than 1'
    }
    else {
        certainQuestion.question = data[number-1].question;
        certainQuestion.number = parseInt(number);
    }
    return certainQuestion
    }

    function getAnswer(number = ""){
        const specificAnswer = { error: "", answer: "", number: ""
        }
        if(!Number.isInteger(number)){
            specificAnswer.error = 'Answer number needs to be an integer'
        }
        else if(number > 3){
            specificAnswer.error = 'Answer number needs to be less than the number of questions (3)'
        }
        else if(number < 1){
            specificAnswer.error = 'Answer number must be greater than 1'
        }
        else {
            specificAnswer.answer = data[number-1].answer;
            specificAnswer.number = parseInt(number);
        }
        return specificAnswer
        }

        function getQuestionAnswer(number = ""){
            const specificQuestionAnswer = { error: "", question: "", answer: "", number: ""
            }
            if(!Number.isInteger(number)){
                specificQuestionAnswer.error = 'Question number needs to be an integer'
            }
            else if(number > 3){
                specificQuestionAnswer.error = 'Question number needs to be less than the number of questions (3)'
            }
            else if(number < 1){
                specificQuestionAnswer.error = 'Question number must be greater than 1'
            }
            else {
                specificQuestionAnswer.answer = data[number-1].answer;
                specificQuestionAnswer.number = parseInt(number);
            }
            return specificQuestionAnswer
            }



            /*****************************
  Module function testing
******************************/
function testing(category, ...args) {
    console.log(`\n** Testing ${category} **`);
    console.log("-------------------------------");
    for (const o of args) {
      console.log(`-> ${category}${o.d}:`);
      console.log(o.f);
    }
  }
  
  // Set a constant to true to test the appropriate function
  const testGetQs = false;
  const testGetAs = false;
  const testGetQsAs = false;
  const testGetQ = false;
  const testGetA = false;
  const testAdd = false;      // Extra credit
  const testUpdate = false;   // Extra credit
  const testDelete = false;   // Extra credit

  // getQuestions()
if (testGetQs) {
    testing("getQuestions", { d: "()", f: getQuestions() });
  }
  
  // getAnswers()
  if (testGetAs) {
    testing("getAnswers", { d: "()", f: getAnswers() });
  }
  
  // getQuestionsAnswers()
  if (testGetQsAs) {
    testing("getQuestionsAnswers", { d: "()", f: getQuestionsAnswers() });
  }

  // getQuestion()
if (testGetQ) {
    testing(
      "getQuestion",
      { d: "()", f: getQuestion() },      // Extra credit: +1
      { d: "(0)", f: getQuestion(0) },    // Extra credit: +1
      { d: "(1)", f: getQuestion(1) },
      { d: "(4)", f: getQuestion(4) }     // Extra credit: +1
    );
  }
  
  // getAnswer()
  if (testGetA) {
    testing(
      "getAnswer",
      { d: "()", f: getAnswer() },        // Extra credit: +1
      { d: "(0)", f: getAnswer(0) },      // Extra credit: +1
      { d: "(1)", f: getAnswer(1) },
      { d: "(4)", f: getAnswer(4) }       // Extra credit: +1
    );
  }
  
  // getQuestionAnswer()
  if (testGetQA) {
    testing(
      "getQuestionAnswer",
      { d: "()", f: getQuestionAnswer() },    // Extra credit: +1
      { d: "(0)", f: getQuestionAnswer(0) },  // Extra credit: +1
      { d: "(1)", f: getQuestionAnswer(1) },
      { d: "(4)", f: getQuestionAnswer(4) }   // Extra credit: +1
    );
  }

  module.exports = {
      getQuestions,getAnswers,getQuestionsAnswers,getAnswer,getQuestion
  }
  
  **p4-server.js**
  
  const fs = require("fs");
const fastify = require("fastify")();
const { getQuestions,getAnswers,getQuestionsAnswers,getAnswer,getQuestion}

fastify.get("/cit/question", (request, reply) => {
    const questionsToReturn = getQuestions();
    const resultToReturn = JSON.stringify(questionsToReturn);
    reply
    .code(200)
    .header("Content-Type", "application/json; charset=utf-8")
    .send(resultToReturn);
});

fastify.get("/cit/question/:number", (request, reply) => {
    const { numOfQuestion} = request.params;
    const questionsToReturn = getQuestions(numOfQuestion);
    const resultToReturn = JSON.stringify(questionsToReturn);
    reply
    .code(200)
    .header("Content-Type", "application/json; charset=utf-8")
    .send(resultToReturn);
});

fastify.get("/cit/answer/:number", (request, reply) => {
    console.log(request);
    const { numOfQuestion} = request.params;
    const answerToReturn = getAnswer(numOfAnswer);
    const resultToReturn = JSON.stringify(answerToReturn);
    reply
    .code(200)
    .header("Content-Type", "application/json; charset=utf-8")
    .send(resultToReturn);
});

fastify.get("/cit/questionanswer", (request, reply) => {
    const questionAnswerToReturn = getQuestionsAnswers();
    const resultToReturn = JSON.stringify(questionAnswerToReturn);
    reply
    .code(200)
    .header("Content-Type", "application/json; charset=utf-8")
    .send(resultToReturn);
});

fastify.get("/cit/questionanswer/:number", (request, reply) => {
    console.log(request);
    const { numOfquestionAnswer} = request.params;
    const questionAnswerToReturn = getQuestionsAnswers(numOfquestionAnswer);
    const resultToReturn = JSON.stringify(questionAnswerToReturn);
    reply
    .code(200)
    .header("Content-Type", "application/json; charset=utf-8")
    .send(resultToReturn);
});

fastify.get("*", (request, reply) => {
    reply
    .code(200)
    .header("Content-Type", "text/html; charset=utf-8")
    .send("<h1>error: Route not found, statusCode: 404</h1>");
});

const listenIP = "localhost";
const listenPort = 8082;
fastify.listen(listenPort, listenIP, (err, address) => {
    if (err) { console.log(err); process.exit(1);
    }
    console.log(`Server listening on ${address}`);
});
