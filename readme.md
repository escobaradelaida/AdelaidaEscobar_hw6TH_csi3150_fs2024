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
- **`startQuiz()`**: Begins the quiz and shows the first question
- **`startTimer()`**: Starts the timer for each of the questions and updates the counter.
- **`showQuestion()`**: Displays the current question and the options that correspond to that question.
- **`nextQuestion()`**: Moves to the next question regardless of whether the user chose an option or if time is up.
- **`optionSelected()`**: Handles user answer and updates their score.
- **`showResult()`**: Displays the final score at the end of the quiz.


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


