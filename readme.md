# DemoQuizApp Documentation

### Overview

This project is a quiz application built using HTML, CSS, and Javascript. Users have 15 seconds to answer a series of questions based on programming terminology. The app displays each question one by one and will provide immediate feedback, meaning users will not be able to change their answer once selected. Users will then be able to see their score at the end of the quiz.

### File Structure
The app consists of the following files:
- **index.html**: This is the main HTML structure of the application.
- **css/style.css**: This is the styling of the application.
- **js/questions.js**: Contains the list of questions that will be presented to the user. This file will interact with quizApp.js.
- **js/quizApp.js**: This is the main file that will provide the logic to the application. This includes the way questions are handled and the timer.

These files are linked together as such:
- The `index.html` files references both the `style.css` and `quizApp.js` for the actual functionality.
- The `quizApp.js` files interacts with `questions.js` file to load the questions and options for the user.
- The `style.css` file is applied to the `index.html` elements to create the interface.

### Functionality
1. **Start Quiz**: This will display the rules and a start button to being the quiz.
2. **Rules**: A set of instructions explains to the user how the quiz works:
      - Each question has a 15-second time limit.
      - Once an answer is selected, it cannot be undone.
      - Users cannot exit or skip the questions.
3. **Quiz Interface**: Shows the current question, the different answers to select from, and it will show a countdown timer.
4. **Results**: After the quiz is completed, it will display the user's score, which is the number of questions answered correctly out of the total.

### How it works

#### 1. HTML Structure (`index.html`)
The `index.html` file contains the layout for the quiz, such as the start button, instructions, the display area of the questions, and the results. Javascript will add the questions and options.

#### 2. CSS
The `style.css` files provides the styling for the app:
- **Layout**: Defines the overall structure and placement of the questions and options.
- **Buttons**: Styles the "Start Quiz" and answer buttons. 
- **Timer and Progress Bar**: Styles the way the countdown timer and progress bar looks like.
- **Responsive Design**: Makes sure the app looks good on both desktop and mobile screens.

#### 2. Javascript (`quizApp.js`)
The `quizApp.js` handles the main functionality of the quiz.
- **Start Quiz**: This shows the instructions when the quiz starts.
- **Timer**: This is the countdown for each question. If the timer runs out, it will automatically choose an answer (the correct answer is chosen).
- **Next Question**: Moves to the next question once the user selects their answer or if the timer ends.

#### Key Functions:
- **`startTimer()`**: Starts the timer for each of the questions and updates the counter.
```javascript
// control the timer and actions associated to it
function startTimer(time) {
  counter = setInterval(timer, 1000);
  function timer() {
    timeCount.textContent = time; //change the value of timeCount with time value
    time--; //decrement the time value
    if (time < 9) {
      //if timer is less than 9
      let addZero = timeCount.textContent;
      timeCount.textContent = "0" + addZero; //add a 0 before time value
    }
    if (time < 0) {
      //if timer is less than 0
      clearInterval(counter); //clear counter
      timeText.textContent = "Time Off"; //change the time text to time off
      const allOptions = option_list.children.length; //get all option items
      let correcAns = questions[que_count].answer; //get correct answer from array
      for (i = 0; i < allOptions; i++) {
        if (option_list.children[i].textContent == correcAns) {
          //if there is an option which is matched to an array answer
          option_list.children[i].setAttribute("class", "option correct"); //add green color to matched option
          option_list.children[i].insertAdjacentHTML("beforeend", tickIconTag); //add tick icon to matched option
          console.log("Time Off: Auto selected correct answer.");
        }
      }
      for (i = 0; i < allOptions; i++) {
        option_list.children[i].classList.add("disabled"); //once user select an option then disabled all options
      }
      next_btn.classList.add("show"); //show the next button if user selected any option
    }
  }
}
```
Explanation: This will update te displayed time every second. Within the `if (time < 0)`, if the timer reaches 0, it automatically selects the correct answer, clears the timer, disables the options, and will show the "Next" button.

- **`showQuetions()`**: Displays the current question and the options that correspond to that question.
```javascript
function showQuetions(index) {
  const que_text = document.querySelector(".que_text");

  //creating a new span and div tag for question and option and passing the value using array index
  // self exercise: re-write the following using backtick syntax for string in JS instead of concatenation operator
  let que_tag =
    "<span>" +
    questions[index].numb +
    ". " +
    questions[index].question +
    "</span>";
  let option_tag =
    '<div class="option"><span>' +
    questions[index].options[0] +
    "</span></div>" +
    '<div class="option"><span>' +
    questions[index].options[1] +
    "</span></div>" +
    '<div class="option"><span>' +
    questions[index].options[2] +
    "</span></div>" +
    '<div class="option"><span>' +
    questions[index].options[3] +
    "</span></div>";
  que_text.innerHTML = que_tag; //adding new (child) span tag inside que_tag
  option_list.innerHTML = option_tag; //adding new (child) div tag inside option_tag

  const option = option_list.querySelectorAll(".option");

  // set onclick attribute to all available options
  for (i = 0; i < option.length; i++) {
    option[i].setAttribute("onclick", "optionSelected(this)");
  }
}
```
Explanation: It will fetch the question from the array in `questions.js` based on the index and it will generate the HTML to display the question and option to the user.

- **`optionSelected()`**: Handles user answer and updates their score.
```javascript
//if user clicked on option
function optionSelected(answer) {
  clearInterval(counter); //clear counter
  clearInterval(counterLine); //clear counterLine
  let userAns = answer.textContent; //getting user selected option
  let correcAns = questions[que_count].answer; //getting correct answer from array
  const allOptions = option_list.children.length; //getting all option items

  //if user selected option is equal to array's correct answer
  if (userAns == correcAns) {
    userScore += 1; //update total score value increment by 1
    answer.classList.add("correct"); //add green color to correct selected option
    answer.insertAdjacentHTML("beforeend", tickIconTag); //add tick icon to correct selected option
    console.log("Correct Answer");
    console.log("Your correct answers = " + userScore);
  } else {
    answer.classList.add("incorrect"); //add red color to correct selected option
    answer.insertAdjacentHTML("beforeend", crossIconTag); //add cross icon to correct selected option
    console.log("Wrong Answer");

    for (i = 0; i < allOptions; i++) {
      if (option_list.children[i].textContent == correcAns) {
        //if there is an option which is matched to an array answer
        option_list.children[i].setAttribute("class", "option correct"); //add green color to matched option
        option_list.children[i].insertAdjacentHTML("beforeend", tickIconTag); //add tick icon to matched option
        console.log("Auto selected correct answer.");
      }
    }
  }
  for (i = 0; i < allOptions; i++) {
    option_list.children[i].classList.add("disabled"); //once user select an option, disable all options
  }
  next_btn.classList.add("show"); //show the next button if user selected any option
}
```
Explanation: This function will compate the selected option with the correct answer. It will update the score on whether right or wrong, colors the option (green for right, red for wrong), disables the options, and then shows the "Next" button for the user to proceed.

- **`showResult()`**: Displays the final score at the end of the quiz.
```javascript
// display for result box based on user performance
function showResult() {
  info_box.classList.remove("activeInfo"); //hide info box
  quiz_box.classList.remove("activeQuiz"); //hide quiz box
  result_box.classList.add("activeResult"); //show result box
  const scoreText = result_box.querySelector(".score_text");
  if (userScore > 3) {
    // if user scored more than 3
    //create a new span tag and pass the user score number and total question number
    let scoreTag =
      "<span>and congrats! , You got <p>" +
      userScore +
      "</p> out of <p>" +
      questions.length +
      "</p></span>";
    scoreText.innerHTML = scoreTag; //add new span tag inside score_Text
  } else if (userScore > 1) {
    // if user scored more than 1
    let scoreTag =
      "<span>and nice , You got <p>" +
      userScore +
      "</p> out of <p>" +
      questions.length +
      "</p></span>";
    scoreText.innerHTML = scoreTag;
  } else {
    // if user scored less than 1
    let scoreTag =
      "<span>and sorry , You got only <p>" +
      userScore +
      "</p> out of <p>" +
      questions.length +
      "</p></span>";
    scoreText.innerHTML = scoreTag;
  }
}
```
Explanation: This function will hide the quiz box and show the results box. This results box will contain the user's score with a message. These messages are written in HTML so that they can work in conjunction with the `index.html` file. 


#### 3. Questions Data (`questions.js`)
The questions are stored in an array, where each object represents a question with multiple answers and a correct answer. This is where `quizApp.js` pulls the questions and applies it to the `index.html` file.

Example:
```javascript
let questions = [
    {
        numb: 1,
        question: "What does HTML stand for?",
        answer: "Hyper Text Markup Language",
        options: [
            "Hyper Text Preprocessor",
            "Hyper Text Markup Language",
            "Hyper Text Multiple Language",
            "Hyper Tool Multi Language"
        ],
    },
    // More questions here
];
```
- **numb**: The question number.
- **question**: The text of the question.
- **answer**: The correct answer for the question.
- **options**: This an array that contains the answer choices.
  
***

#### References
1. LifeParticle. *Markdown Cheatsheet*. Github. Retrieved from [https://github.com/lifeparticle/Markdown-Cheatsheet](https://github.com/lifeparticle/Markdown-Cheatsheet)

2. Adam P. *Markdown Cheatsheet*. Github. Retrieved from [https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)


