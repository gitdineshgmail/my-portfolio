
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Dinesh's | Portfolio</title>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Poppins', sans-serif;
    }
    body {
      background-color: #ffffff;
      color: #111111;
      line-height: 1.6;
    }
    header {
      background: #1e88e5;
      color: white;
      padding: 2rem;
      text-align: center;
    }
    header h1 {
      font-size: 2.5rem;
    }
    header p {
      font-size: 1.2rem;
    }
    section {
      padding: 2rem;
      max-width: 900px;
      margin: auto;
    }
    .services, .portfolio {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 1.5rem;
    }
    .card {
      background: #f2f2f2;
      border-radius: 10px;
      padding: 1.5rem;
      box-shadow: 0 2px 10px rgba(0,0,0,0.1);
    }
    .portfolio img {
      width: 100%;
      border-radius: 8px;
    }
    footer {
      background: #1e88e5;
      color: white;
      text-align: center;
      padding: 1.5rem;
      margin-top: 2rem;
    }
    a.button {
      display: inline-block;
      background: #1e88e5;
      color: white;
      padding: 0.7rem 1.5rem;
      border-radius: 5px;
      margin-top: 1rem;
      text-decoration: none;
      font-weight: bold;
    }
    #chatbot {
      position: fixed;
      bottom: 20px;
      right: 20px;
      background: #ffffff;
      border: 1px solid #ccc;
      width: 320px;
      height: 400px;
      border-radius: 10px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.2);
      display: flex;
      flex-direction: column;
      overflow: hidden;
      color: #111111;
    }
    #chat-header {
      background: #1e88e5;
      color: white;
      padding: 0.75rem;
      font-weight: bold;
    }
    #chat-body {
      flex: 1;
      padding: 1rem;
      overflow-y: auto;
      font-size: 0.9rem;
    }
    #chat-input {
      display: flex;
      border-top: 1px solid #ddd;
    }
    #chat-input input {
      flex: 1;
      padding: 0.5rem;
      border: none;
      outline: none;
      background: #f7f7f7;
      color: #111111;
    }
    #chat-input button {
      padding: 0.5rem 1rem;
      background: #1e88e5;
      color: white;
      border: none;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <header>
    <h1>Dinesh</h1>
    <p>Creative Designer & Chatbot Developer</p>
  </header>

  <section>
    <h2>About Me</h2>
    <p>I specialize in logo design, video editing, chatbot development, and Arduino-based solutions. With over 7 years of experience, I deliver creative and efficient digital solutions.</p>
  </section>

  <section>
    <h2>Services</h2>
    <div class="services">
      <div class="card">🎨 Logo Design</div>
      <div class="card">🎞️ Video Editing</div>
      <div class="card">🤖 AI Chatbots</div>
      <div class="card">🔌 Arduino Projects</div>
      <div class="card">🖼️ Image Enhancement</div>
    </div>
  </section>

  <section>
    <h2>Portfolio</h2>
    <div class="portfolio">
      <div class="card">
        <img src="https://via.placeholder.com/300x200" alt="Project 1">
        <p>Project Title 1</p>
      </div>
      <div class="card">
        <img src="https://via.placeholder.com/300x200" alt="Project 2">
        <p>Project Title 2</p>
      </div>
    </div>
  </section>

  <section>
    <h2>Contact Me</h2>
    <p>If you like my work, feel free to contact me on Fiverr.</p>
    <a href="https://www.fiverr.com/@dinesh_dishan" class="button" target="_blank">Visit My Fiverr</a>
  </section>

  <div id="chatbot">
    <div id="chat-header">Chat with AI</div>
    <div id="chat-body">
      <p><em>Hi! I am Dinesh's assintans.🎤 Voice supported! Click the mic or type your message below.</em></p>
    </div>
    <div id="chat-input">
      <input type="text" placeholder="Type a message or use voice..." />
      <button>🎙️</button>
    </div>
  </div>

  <footer>
    <p>&copy; 2025 Dinesh. All rights reserved.</p>
  </footer>

  <script>
    const inputField = document.querySelector('#chat-input input');
    const sendButton = document.querySelector('#chat-input button');
    const chatBody = document.querySelector('#chat-body');

    const API_KEY = "YOUR_OPENAI_API_KEY_HERE"; // Replace with your actual OpenAI API key

    async function sendMessage(text) {
      if (!text.trim()) return;

      const userMsg = document.createElement('p');
      userMsg.textContent = "🧑‍💻 You: " + text;
      chatBody.appendChild(userMsg);
      chatBody.scrollTop = chatBody.scrollHeight;

      const loadingMsg = document.createElement('p');
      loadingMsg.textContent = "🤖 Thinking...";
      chatBody.appendChild(loadingMsg);

      try {
        const response = await fetch("https://api.openai.com/v1/chat/completions", {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
            "Authorization": `Bearer ${API_KEY}`
          },
          body: JSON.stringify({
            model: "gpt-3.5-turbo",
            messages: [{ role: "user", content: text }],
            max_tokens: 200
          })
        });

        const data = await response.json();
        loadingMsg.remove();

        const botMsg = document.createElement('p');
        botMsg.textContent = "🤖 Bot: " + data.choices[0].message.content.trim();
        chatBody.appendChild(botMsg);
        chatBody.scrollTop = chatBody.scrollHeight;

      } catch (error) {
        loadingMsg.remove();
        const errMsg = document.createElement('p');
        errMsg.textContent = "⚠️ Error getting response.";
        chatBody.appendChild(errMsg);
      }
    }

    // Text input send
    inputField.addEventListener('keydown', e => {
      if (e.key === 'Enter') {
        sendMessage(inputField.value);
        inputField.value = '';
      }
    });

    // Voice input send
    sendButton.addEventListener('click', () => {
      const recognition = new (window.SpeechRecognition || window.webkitSpeechRecognition)();
      recognition.lang = 'en-US';
      recognition.start();
      recognition.onresult = event => {
        const voiceText = event.results[0][0].transcript;
        inputField.value = voiceText;
        sendMessage(voiceText);
      };
    });
  </script>
</body>
</html>
