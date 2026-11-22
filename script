// Interacciones de la unidad didáctica Explora Animalia

const menuToggle = document.getElementById("menuToggle");
const mainNav = document.getElementById("mainNav");

menuToggle.addEventListener("click", () => {
  const isOpen = mainNav.classList.toggle("open");
  menuToggle.setAttribute("aria-expanded", String(isOpen));
  menuToggle.textContent = isOpen ? "✕" : "☰";
});

mainNav.querySelectorAll("a").forEach(link => {
  link.addEventListener("click", () => {
    mainNav.classList.remove("open");
    menuToggle.setAttribute("aria-expanded", "false");
    menuToggle.textContent = "☰";
  });
});

// Reto breve de clasificación
const challenges = [
  {
    emoji: "🐬",
    question: "El delfín vive en el agua y tiene aletas. ¿A qué grupo pertenece?",
    options: ["Pez", "Mamífero", "Reptil"],
    answer: "Mamífero",
    explanation: "¡Correcto! El delfín respira mediante pulmones y las hembras alimentan a sus crías con leche. Es un mamífero."
  },
  {
    emoji: "🦋",
    question: "La mariposa tiene exoesqueleto, tres pares de patas y alas. ¿A qué grupo pertenece?",
    options: ["Molusco", "Artrópodo", "Anélido"],
    answer: "Artrópodo",
    explanation: "¡Muy bien! Las mariposas son insectos, y los insectos pertenecen al filo de los artrópodos."
  },
  {
    emoji: "🐸",
    question: "La rana suele tener una fase larvaria acuática y experimenta metamorfosis. ¿A qué grupo pertenece?",
    options: ["Anfibio", "Reptil", "Ave"],
    answer: "Anfibio",
    explanation: "¡Exacto! Muchas especies de anfibios presentan metamorfosis y una relación estrecha con ambientes húmedos."
  }
];

let challengeIndex = 0;
let challengeAnswered = false;

const challengeEmoji = document.getElementById("challengeEmoji");
const challengeQuestion = document.getElementById("challengeQuestion");
const challengeOptions = document.getElementById("challengeOptions");
const challengeFeedback = document.getElementById("challengeFeedback");
const challengeCount = document.getElementById("challengeCount");
const nextChallenge = document.getElementById("nextChallenge");

function renderChallenge() {
  const item = challenges[challengeIndex];
  challengeAnswered = false;

  challengeEmoji.textContent = item.emoji;
  challengeQuestion.textContent = item.question;
  challengeCount.textContent = `CASO 0${challengeIndex + 1} / 03`;

  challengeFeedback.textContent =
    "Selecciona una respuesta para comprobar tu razonamiento.";

  challengeFeedback.className = "feedback";
  nextChallenge.disabled = true;

  nextChallenge.innerHTML =
    challengeIndex === challenges.length - 1
      ? 'Volver al inicio <span>↻</span>'
      : 'Siguiente caso <span>→</span>';

  challengeOptions.innerHTML = "";

  item.options.forEach(option => {
    const button = document.createElement("button");

    button.className = "answer-option";
    button.type = "button";
    button.textContent = option;

    button.addEventListener("click", () => {
      chooseChallengeAnswer(option, button);
    });

    challengeOptions.appendChild(button);
  });
}

function chooseChallengeAnswer(option, selectedButton) {
  if (challengeAnswered) return;

  challengeAnswered = true;

  const item = challenges[challengeIndex];

  const buttons = [
    ...challengeOptions.querySelectorAll("button")
  ];

  buttons.forEach(button => {
    button.disabled = true;

    if (button.textContent === item.answer) {
      button.classList.add("correct");
    }
  });

  if (option === item.answer) {
    challengeFeedback.textContent = item.explanation;
    challengeFeedback.className = "feedback good";
  } else {
    selectedButton.classList.add("incorrect");

    challengeFeedback.textContent =
      `No exactamente. La respuesta correcta es ${item.answer}. ${item.explanation}`;

    challengeFeedback.className = "feedback bad";
  }

  nextChallenge.disabled = false;
}

nextChallenge.addEventListener("click", () => {
  challengeIndex = (challengeIndex + 1) % challenges.length;
  renderChallenge();
});

renderChallenge();

// Evaluación de cierre
const quizForm = document.getElementById("quizForm");
const quizResult = document.getElementById("quizResult");

const correctAnswers = {
  q1: "b",
  q2: "c",
  q3: "b",
  q4: "a",
  q5: "b"
};

quizForm.addEventListener("submit", event => {
  event.preventDefault();

  const data = new FormData(quizForm);
  let score = 0;

  const unanswered = Object.keys(correctAnswers).filter(
    key => !data.get(key)
  );

  if (unanswered.length) {
    quizResult.hidden = false;

    quizResult.innerHTML = `
      <h3>Te faltan respuestas</h3>
      <p>Responde las ${unanswered.length} pregunta(s) pendiente(s) antes de calificar.</p>
    `;

    quizResult.scrollIntoView({
      behavior: "smooth",
      block: "center"
    });

    return;
  }

  Object.entries(correctAnswers).forEach(([key, answer]) => {
    if (data.get(key) === answer) {
      score++;
    }
  });

  const message = score === 5
    ? "¡Excelente! Demuestras una comprensión sólida de los conceptos trabajados."
    : score >= 3
      ? "¡Buen trabajo! Revisa la retroalimentación de clase y refuerza los temas que te generaron dudas."
      : "Sigue explorando los módulos y vuelve a intentarlo. Aprender también implica revisar y corregir.";

  quizResult.hidden = false;

  quizResult.innerHTML = `
    <h3>Resultado: ${score} de 5 respuestas correctas</h3>
    <p>${message}</p>
  `;

  quizResult.scrollIntoView({
    behavior: "smooth",
    block: "center"
  });
});

document.getElementById("resetQuiz").addEventListener("click", () => {
  quizResult.hidden = true;
  quizResult.innerHTML = "";
});
