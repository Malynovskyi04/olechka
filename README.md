<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Приглашение на свидание</title>
  <style>
    /* Основные стили */
    body {
      display: flex;
      align-items: center;
      justify-content: center;
      height: 100vh;
      font-family: Arial, sans-serif;
      margin: 0;
      background: radial-gradient(circle, #2a3a58, #1e2a3a); /* Светлое ночное небо с фиолетовым оттенком */
      color: #ffffff;
      overflow: hidden;
      position: relative;
    }

    /* Полупрозрачный слой для улучшенной видимости */
    .overlay {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0, 0, 0, 0.5); /* Черный полупрозрачный слой */
      z-index: 1;
    }

    /* Центрирование контейнера */
    .container {
      width: 350px;
      height: 350px;
      text-align: center;
      padding: 30px;
      border: 3px solid #fff;
      border-radius: 15px;
      background-color: rgba(0, 0, 0, 0.7); /* Полупрозрачный фон */
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      z-index: 10;
    }

    /* Стили для кнопок */
    .button {
      padding: 10px 20px;
      margin: 10px;
      font-size: 16px;
      cursor: pointer;
      border: 1px solid #333;
      border-radius: 5px;
      background-color: #ffffff;
      color: #333;
      position: relative;
      transition: transform 0.3s ease; /* Плавный переход для движения */
    }

    /* Скрытие блока */
    .hidden {
      display: none;
    }
  </style>
</head>
<body>

  <!-- Полупрозрачный слой поверх фона -->
  <div class="overlay"></div>

  <!-- Квадрат с вопросом и кнопками -->
  <div class="container" id="inviteBox">
    <p>Мы идем на свидание?</p>
    <button class="button" id="yesButton">Да</button>
    <button class="button" id="noButton">Нет</button>
    <button class="button" id="sickButton">Я заболела</button>
    <button class="button" id="examButton">У меня экзамены</button>
  </div>

  <!-- Квадрат для выбора даты и времени -->
  <div class="container hidden" id="formBox">
    <p>Выбирай дату и время:</p>
    <label for="date">Дата:</label>
    <input type="date" id="date"><br><br>
    <label for="time">Время:</label>
    <input type="time" id="time"><br><br>
    <button class="button" id="sendButton">Отправить</button>
  </div>

  <script>
    // Получаем элементы кнопок и блоков
    const noButton = document.getElementById("noButton");
    const yesButton = document.getElementById("yesButton");
    const sickButton = document.getElementById("sickButton");
    const examButton = document.getElementById("examButton");
    const inviteBox = document.getElementById("inviteBox");
    const formBox = document.getElementById("formBox");
    const sendButton = document.getElementById("sendButton");

    // Обработка нажатия на "Да" и запуск анимаций
    yesButton.addEventListener("click", () => {
      inviteBox.classList.add("hidden");
      formBox.classList.remove("hidden");
    });

    // Функция для того, чтобы кнопки уходили по отдельности
    function moveButtonAway(button) {
      const randomX = Math.random() * 200 - 100; // Случайное смещение по оси X
      const randomY = Math.random() * 200 - 100; // Случайное смещение по оси Y
      button.style.transform = `translate(${randomX}px, ${randomY}px)`; // Применяем смещение
    }

    // Добавляем обработчики событий для кнопок "Нет", "Я заболела" и "У меня экзамены"
    [noButton, sickButton, examButton].forEach(button => {
      button.addEventListener('mouseenter', () => {
        moveButtonAway(button);
      });

      button.addEventListener('click', () => {
        alert("Неправильный ответ! Попробуй снова)");  // Выводим единое сообщение
      });
    });

    // Обработка нажатия на кнопку "Да" и скрытие блока
    yesButton.addEventListener("click", () => {
      inviteBox.classList.add("hidden");
      formBox.classList.remove("hidden");
    });

    // Проверка, если устройство мобильное
    function isMobile() {
      return /Mobi|Android|iPhone|iPad|iPod/i.test(navigator.userAgent);
    }

    // Обработка отправки данных при нажатии на кнопку "Отправить"
    sendButton.addEventListener("click", () => {
      const date = document.getElementById("date").value;
      const time = document.getElementById("time").value;

      if (!date || !time) {
        alert("Пожалуйста, выберите дату и время.");
        return;
      }

      const email = "kiril20112004@gmail.com"; // Ваш адрес почты
      const subject = "Запрос на свидание"; // Тема письма
      const body = `Выбрана дата свидания: ${date}, время: ${time}`; // Тело письма

      if (isMobile()) {
        // Если мобильное устройство, открываем почтовое приложение
        const mailtoLink = `mailto:${email}?subject=${encodeURIComponent(subject)}&body=${encodeURIComponent(body)}`;
        window.location.href = mailtoLink;
      } else {
        // Для ПК открываем Gmail в браузере
        const mailtoLink = `https://mail.google.com/mail/?view=cm&fs=1&to=${email}&su=${encodeURIComponent(subject)}&body=${encodeURIComponent(body)}`;
        window.location.href = mailtoLink;
      }
    });
  </script>

</body>
</html>
