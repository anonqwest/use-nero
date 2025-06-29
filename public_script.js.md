---
created: 2025-06-30T03:10:59+06:00
modified: 2025-06-30T03:11:26+06:00
---

# public/script.js

function goToGreeting() {
  const name = document.getElementById("username").value.trim();
  if (!name) return alert("Введите имя");

  document.getElementById("name-section").style.display = "none";
  document.getElementById("greeting-text").innerText =
    `Здравствуйте, ${name}! Не желаете научиться пользоваться нейросетью?`;
  document.getElementById("greeting-section").style.display = "block";
}

function sayLater() {
  alert("Хорошо, я всегда буду здесь и готов помочь тебе с твоими задачами.");
}

function goToGoal() {
  document.getElementById("greeting-section").style.display = "none";
  document.getElementById("goal-section").style.display = "block";
}

async function askAI() {
  const goal = document.getElementById("goal").value.trim();
  if (!goal) return alert("Напиши, что ты хочешь реализовать");

  const responseBox = document.getElementById("response");
  responseBox.innerText = "Думаю...";

  try {
    const res = await fetch("/chat", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({ message: goal }),
    });
    const data = await res.json();
    responseBox.innerText = data.reply || "Ответа нет...";
  } catch (err) {
    responseBox.innerText = "Произошла ошибка. Попробуй позже.";
  }
}
