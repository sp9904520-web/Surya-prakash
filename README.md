<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Student Portfolio</title>

  <!-- EmailJS SDK -->
  <script type="text/javascript" src="https://cdn.emailjs.com/dist/email.min.js"></script>
  <script>
    (function () {
      emailjs.init("YOUR_PUBLIC_KEY"); // replace with your EmailJS Public Key
    })();
  </script>

  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      background: #f4f4f4;
      color: #333;
    }

    header {
      background: #333;
      color: #fff;
      padding: 1rem;
    }

    .navbar {
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;
    }

    .navbar .logo {
      font-size: 1.5rem;
      font-weight: bold;
    }

    .nav-links {
      list-style: none;
      display: flex;
      gap: 20px;
    }

    .nav-links li a {
      text-decoration: none;
      color: #fff;
    }

    .menu-toggle {
      display: none;
    }

    section {
      padding: 40px 20px;
      max-width: 900px;
      margin: auto;
    }

    .hero-content h1 span {
      color: #007bff;
    }

    .btn {
      display: inline-block;
      margin-top: 20px;
      background: #007bff;
      color: white;
      padding: 10px 20px;
      border: none;
      border-radius: 5px;
      text-decoration: none;
    }

    .about-content {
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    .about-content img {
      max-width: 200px;
      border-radius: 50%;
      margin-bottom: 20px;
    }

    .project-grid {
      display: grid;
      gap: 20px;
    }

    .project-card {
      background: white;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    }

    form input, form textarea {
      width: 100%;
      margin-bottom: 15px;
      padding: 10px;
      border-radius: 5px;
      border: 1px solid #ccc;
    }

    form button {
      background: #007bff;
      color: white;
      padding: 10px 20px;
      border: none;
      border-radius: 5px;
    }

    footer {
      text-align: center;
      padding: 20px;
      background: #333;
      color: #fff;
    }

    /* Quiz styles */
    .quiz-container {
      background: white;
      padding: 20px;
      border-radius: 10px;
      max-width: 500px;
      margin: auto;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    }

    .question {
      font-size: 20px;
      margin-bottom: 20px;
    }

    .option {
      margin-bottom: 10px;
    }

    #result {
      margin-top: 20px;
      font-weight: bold;
    }

    /* Blog styles */
    .post {
      background: white;
      padding: 15px;
      margin-bottom: 20px;
      border-radius: 8px;
      box-shadow: 0 0 5px rgba(0, 0, 0, 0.1);
    }

    .post h2 {
      margin: 0 0 10px;
    }

    .post small {
      color: gray;
      font-size: 12px;
    }
  </style>
</head>

<body>

  <!-- Navbar -->
  <header>
    <nav class="navbar">
      <div class="logo">MyPortfolio</div>
      <ul class="nav-links">
        <li><a href="#home">Home</a></li>
        <li><a href="#about">About</a></li>
        <li><a href="#projects">Projects</a></li>
        <li><a href="#quiz">Quiz</a></li>
        <li><a href="#blog">Blog</a></li>
        <li><a href="#contact">Contact</a></li>
      </ul>
    </nav>
  </header>

  <!-- Hero -->
  <section id="home" class="hero">
    <div class="hero-content">
      <h1>Hello, I'm <span>SURYA PRAKASH</span></h1>
      <p>I am a student</p>
      <a href="#projects" class="btn">View My Work</a>
    </div>
  </section>

  <!-- About -->
  <section id="about">
    <h2>About Me</h2>
    <div class="about-content">
      <img src="IMG_1000033005.jpg" alt="Profile Photo">
      <p>
        I am a student enthusiastic about technology and design. I love building interactive,
        user-friendly web applications and exploring new tools in the tech world.
      </p>
    </div>
  </section>

  <!-- Projects -->
  <section id="projects">
    <h2>My Projects</h2>
    <div class="project-grid">
      <div class="project-card">
        <h3>Project 1</h3>
        <p>A simple responsive website.</p>
      </div>
      <div class="project-card">
        <h3>Project 2</h3>
        <p>JavaScript-based quiz app.</p>
      </div>
      <div class="project-card">
        <h3>Project 3</h3>
        <p>Personal blog with CMS.</p>
      </div>
    </div>
  </section>

  <!-- Quiz Section -->
  <section id="quiz">
    <h2>Random Quiz</h2>
    <div class="quiz-container">
      <div class="question" id="question">Loading question...</div>
      <div id="options"></div>
      <button onclick="checkAnswer()">Submit</button>
      <div id="result"></div>
    </div>
  </section>

  <!-- Blog Section -->
  <section id="blog">
    <h2>My Blog</h2>
    <div class="container" id="postsContainer"></div>
  </section>

  <!-- Contact -->
  <section id="contact">
    <h2>Contact Me</h2>
    <form id="contact-form">
      <input type="text" id="name" name="user_name" placeholder="Your Name" required>
      <input type="email" id="email" name="user_email" placeholder="Your Email" required>
      <textarea id="message" name="message" placeholder="Your Message" required></textarea>
      <button type="submit">Send</button>
    </form>
    <p id="form-status"></p>
  </section>

  <!-- Footer -->
  <footer>
    <p>&copy; 2025 SURYA PRAKASH | All rights reserved</p>
  </footer>

  <!-- Script -->
  <script>
    // Quiz
    const quizData = [
      {
        question: "What is the capital of France?",
        options: ["Berlin", "Madrid", "Paris", "Rome"],
        answer: "Paris"
      },
      {
        question: "What is 2 + 2?",
        options: ["3", "4", "5", "6"],
        answer: "4"
      },
      {
        question: "Which planet is known as the Red Planet?",
        options: ["Earth", "Mars", "Jupiter", "Venus"],
        answer: "Mars"
      },
      {
        question: "Who wrote 'Romeo and Juliet'?",
        options: ["Mark Twain", "William Shakespeare", "Charles Dickens", "Jane Austen"],
        answer: "William Shakespeare"
      }
    ];

    const questionEl = document.getElementById("question");
    const optionsEl = document.getElementById("options");
    const resultEl = document.getElementById("result");

    const currentQuiz = quizData[Math.floor(Math.random() * quizData.length)];

    function loadQuiz() {
      questionEl.textContent = currentQuiz.question;
      optionsEl.innerHTML = "";
      resultEl.textContent = "";

      currentQuiz.options.forEach((option, index) => {
        const optionHTML = `
          <div class="option">
            <input type="radio" name="answer" id="option${index}" value="${option}">
            <label for="option${index}">${option}</label>
          </div>
        `;
        optionsEl.innerHTML += optionHTML;
      });
    }

    function checkAnswer() {
      const selected = document.querySelector('input[name="answer"]:checked');
      if (!selected) {
        resultEl.textContent = "Please select an answer!";
        resultEl.style.color = "red";
        return;
      }
      if (selected.value === currentQuiz.answer) {
        resultEl.textContent = "Correct!";
        resultEl.style.color = "green";
      } else {
        resultEl.textContent = `Incorrect. The correct answer was "${currentQuiz.answer}".`;
        resultEl.style.color = "red";
      }
    }

    loadQuiz();

    // Blog
    function loadPosts() {
      const postsContainer = document.getElementById("postsContainer");
      const posts = JSON.parse(localStorage.getItem("blogPosts")) || [
        { title: "Welcome to my blog", content: "This is a sample blog post.", date: new Date() }
      ];
      postsContainer.innerHTML = "";
      posts.reverse().forEach(post => {
        const postEl = document.createElement("div");
        postEl.classList.add("post");
        postEl.innerHTML = `
          <h2>${post.title}</h2>
          <small>${new Date(post.date).toLocaleString()}</small>
          <p>${post.content}</p>
        `;
        postsContainer.appendChild(postEl);
      });
    }

    loadPosts();
  </script>
</body>
</html>
