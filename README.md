<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Student Portfolio</title>
  <link rel="stylesheet" href="style.css">
  <script defer src="script.js"></script>
  <!-- EmailJS SDK -->
  <script type="text/javascript" src="https://cdn.emailjs.com/dist/email.min.js"></script>
  <script>
    (function () {
      emailjs.init("YOUR_PUBLIC_KEY"); // replace with your EmailJS Public Key
    })();
  </script>
  <style>
    /* Shared styling */
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      background: #f9f9f9;
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
    }
    .navbar .nav-links {
      list-style: none;
      display: flex;
      gap: 15px;
    }
    .navbar a {
      color: white;
      text-decoration: none;
    }
    section {
      padding: 40px 20px;
    }

    /* Quiz styling */
    .quiz-container {
      max-width: 600px;
      margin: 0 auto;
      background-color: #fff;
      padding: 20px;
      border-radius: 8px;
      box-shadow: 0 4px 8px rgba(0,0,0,0.1);
    }
    .question { font-size: 1.5em; margin-bottom: 20px; }
    .answer-button {
      display: block;
      background-color: #4CAF50;
      color: white;
      border: none;
      padding: 10px;
      margin: 5px 0;
      width: 100%;
      font-size: 1.1em;
      cursor: pointer;
      border-radius: 5px;
      transition: background-color 0.3s;
    }
    .answer-button:hover { background-color: #45a049; }
    .hidden { display: none; }

    /* Blog styling */
    .container {
      max-width: 800px;
      margin: 20px auto;
      padding: 10px;
    }
    .post {
      background: white;
      padding: 15px;
      margin-bottom: 20px;
      border-radius: 8px;
      box-shadow: 0 0 5px rgba(0,0,0,0.1);
    }
    .post h2 { margin: 0 0 10px; }
    .post small { color: gray; font-size: 12px; }
  </style>
</head>
<body>
  <!-- Navbar -->
  <header>
    <nav class="navbar">
      <div class="logo">MyPortfolio</div>
      <ul class="nav-links" id="nav-links">
        <li><a href="#home">Home</a></li>
        <li><a href="#about">About</a></li>
        <li><a href="#projects">Projects</a></li>
        <li><a href="#quiz">Quiz</a></li>
        <li><a href="#blog">Blog</a></li>
        <li><a href="#contact">Contact</a></li>
      </ul>
      <div class="menu-toggle" id="menu-toggle">&#9776;</div>
    </nav>
  </header>

  <!-- Hero -->
  <section id="home" class="hero">
    <div class="hero-content">
      <h1>Hello, I'm <span>MR__SURYA_PRAKRSH_G</span></h1>
      <p>I am the student</p>
      <a href="#projects" class="btn">View My Work</a>
    </div>
  </section>

  <!-- About -->
  <section id="about">
    <h2>About Me</h2>
    <div class="about-content">
      <img src="IMG_ 1000033005.jpg" alt="Profile Photo" width="200">
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
      <div class="project-card"><h3>Project 1</h3><p>A simple responsive website.</p></div>
      <div class="project-card"><h3>Project 2</h3><p>JavaScript-based quiz app.</p></div>
      <div class="project-card"><h3>Project 3</h3><p>Personal blog with CMS.</p></div>
    </div>
  </section>

  <!-- Quiz -->
  <section id="quiz">
    <h2>Random Quiz</h2>
    <div class="quiz-container">
      <div id="quiz-box">
        <div id="question" class="question"></div>
        <div id="answers" class="answers"></div>
        <button onclick="nextQuestion()" class="answer-button hidden" id="next-button">Next Question</button>
      </div>
      <div id="result" class="hidden"></div>
    </div>
  </section>

  <!-- Blog -->
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
    <p>&copy; 2025MR__SURYA_PRAKASH_G| All rights reserved</p>
  </footer>

  <script>
    /* Quiz Script */
    const questions = [
      { question: "What is the capital of France?", answers: ["Berlin","Madrid","Paris","Rome"], correctAnswer: "Paris" },
      { question: "Which planet is known as the Red Planet?", answers: ["Earth","Mars","Venus","Jupiter"], correctAnswer: "Mars" },
      { question: "Who wrote 'Romeo and Juliet'?", answers: ["Shakespeare","Dickens","Austen","Hemingway"], correctAnswer: "Shakespeare" },
      { question: "What is the largest ocean on Earth?", answers: ["Atlantic Ocean","Indian Ocean","Pacific Ocean","Arctic Ocean"], correctAnswer: "Pacific Ocean" },
      { question: "Which element has the chemical symbol 'O'?", answers: ["Oxygen","Gold","Osmium","Ozone"], correctAnswer: "Oxygen" }
    ];
    let score = 0, currentQuestionIndex = 0;
    function shuffleArray(array){ for(let i=array.length-1;i>0;i--){const j=Math.floor(Math.random()*(i+1));[array[i],array[j]]=[array[j],array[i]];}}
    function loadQuestion(){
      const q=questions[currentQuestionIndex];
      document.getElementById("question").textContent=q.question;
      const answers=[...q.answers]; shuffleArray(answers);
      const answersDiv=document.getElementById("answers"); answersDiv.innerHTML="";
      answers.forEach(a=>{
        const btn=document.createElement("button");
        btn.textContent=a; btn.classList.add("answer-button");
        btn.onclick=()=>checkAnswer(a);
        answersDiv.appendChild(btn);
      });
      document.getElementById("next-button").classList.add("hidden");
    }
    function checkAnswer(answer){
      const q=questions[currentQuestionIndex];
      const resultDiv=document.getElementById("result");
      if(answer===q.correctAnswer){ score++; resultDiv.textContent="Correct!"; }
      else { resultDiv.textContent=`Incorrect! The correct answer was ${q.correctAnswer}.`; }
      document.getElementById("next-button").classList.remove("hidden");
      resultDiv.classList.remove("hidden");
    }
    function nextQuestion(){
      currentQuestionIndex++;
      if(currentQuestionIndex<questions.length){ loadQuestion(); document.getElementById("result").classList.add("hidden"); }
      else{ document.getElementById("quiz-box").innerHTML=`<h2>Quiz Complete!</h2><p>Your final score is ${score} out of ${questions.length}.</p>`; }
    }
    loadQuestion();

    /* Blog Script */
    function loadPosts(){
      const postsContainer=document.getElementById("postsContainer");
      const posts=JSON.parse(localStorage.getItem("blogPosts"))||[];
      postsContainer.innerHTML="";
      posts.reverse().forEach(post=>{
        const postEl=document.createElement("div");
        postEl.classList.add("post");
        postEl.innerHTML=`<h2>${post.title}</h2><small>${new Date(post.date).toLocaleString()}</small><p>${post.content}</p>`;
        postsContainer.appendChild(postEl);
      });
    }
    loadPosts();
  </script>
</body>
</html>
