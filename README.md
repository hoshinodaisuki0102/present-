<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>사라진 생일선물</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>

<div id="game-container">
    <h1>당신의 생일선물이 사라졌습니다!</h1>
    <p>대신 의문의 초대장이 도착했습니다.</p>
    <button id="start-btn">📜 초대장 받기</button>

    <div id="quiz-container" class="hidden">
        <h2 id="quiz-question"></h2>
        <input type="text" id="quiz-answer" placeholder="정답 입력">
        <button id="submit-btn">제출</button>
        <p id="feedback"></p>
    </div>
</div>

<script src="script.js"></script>
</body>
</html>
@import url('https://fonts.googleapis.com/css2?family=Jua&display=swap');

body {
    font-family: 'Jua', sans-serif;
    text-align: center;
    background-color: #f8f9fa;
}

#game-container {
    max-width: 500px;
    margin: 50px auto;
    padding: 20px;
    background: white;
    border-radius: 10px;
    box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.2);
}

h1 {
    color: #ff6b6b;
}

button {
    padding: 10px 20px;
    font-size: 18px;
    border: none;
    background-color: #ff6b6b;
    color: white;
    border-radius: 5px;
    cursor: pointer;
    margin-top: 10px;
}

button:hover {
    background-color: #ff4757;
}

input {
    width: 80%;
    padding: 8px;
    font-size: 16px;
    margin-top: 10px;
    text-align: center;
}

.hidden {
    display: none;
}
const startBtn = document.getElementById("start-btn");
const quizContainer = document.getElementById("quiz-container");
const questionElement = document.getElementById("quiz-question");
const answerInput = document.getElementById("quiz-answer");
const submitBtn = document.getElementById("submit-btn");
const feedbackElement = document.getElementById("feedback");

const quizzes = [
    { question: "다음 숫자와 관련있는 이름은? 19021216 1920928", answer: "유관순 열사" },
    { question: "모든 정수를 다 곱하면 얼마일까요?", answer: "0" },
    { question: "1919년 일제의 조선 식민지배를 반대하며 약 3000명의 군중이 대한독립을 외친 장소는 어디일까요?", answer: "아우내장터" },
    { question: "다음 알파벳으로 알맞은 단어를 조합하시오: yadhtrib", answer: "birthday" },
    { question: "1919년 3·1 운동 때 발표된 기미독립선언서에 서명한 위인들을 일컫는 말은?", answer: "민족대표 33인" },
    { question: "가 수도(3.1L/분)와 나 수도(0.6L/분)로 49L의 물통을 채우려면 몇 분 몇 초 걸릴까요?", answer: "19분 36초" },
    { question: "다음 글자를 재배열하시오: '울해상힉채'", answer: "생일축하해" }
];

let currentQuiz = 0;

startBtn.addEventListener("click", () => {
    startBtn.style.display = "none";
    quizContainer.classList.remove("hidden");
    showQuestion();
});

submitBtn.addEventListener("click", () => {
    checkAnswer();
});

answerInput.addEventListener("keypress", (event) => {
    if (event.key === "Enter") {
        checkAnswer();
    }
});

function showQuestion() {
    if (currentQuiz < quizzes.length) {
        questionElement.textContent = quizzes[currentQuiz].question;
        answerInput.value = "";
        feedbackElement.textContent = "";
    } else {
        quizContainer.innerHTML = "<h2>🎉 축하합니다! 선물을 찾았습니다! 🎁</h2>";
    }
}

function checkAnswer() {
    let userAnswer = answerInput.value.trim().replace(/\s+/g, "");
    let correctAnswer = quizzes[currentQuiz].answer.replace(/\s+/g, "");

    if (userAnswer === correctAnswer) {
        feedbackElement.textContent = "✅ 정답입니다!";
        feedbackElement.style.color = "green";
        currentQuiz++;
        setTimeout(showQuestion, 1000);
    } else {
        feedbackElement.textContent = "❌ 오답입니다. 다시 시도하세요!";
        feedbackElement.style.color = "red";
    }
}
