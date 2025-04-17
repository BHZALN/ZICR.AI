<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Vellure AI Chat</title>
  <style>
    body {
      margin: 0;
      font-family: "Segoe UI", sans-serif;
      background: linear-gradient(135deg, #1a1a2e, #16213e, #0f3460);
      color: white;
      height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
    }

    .chat-container {
      background: rgba(255, 255, 255, 0.05);
      border: 1px solid rgba(255, 255, 255, 0.1);
      border-radius: 20px;
      width: 90%;
      max-width: 500px;
      height: 80vh;
      display: flex;
      flex-direction: column;
      overflow: hidden;
      box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
      backdrop-filter: blur(10px);
    }

    .messages {
      flex: 1;
      padding: 20px;
      overflow-y: auto;
      display: flex;
      flex-direction: column;
      gap: 12px;
    }

    .message {
      max-width: 80%;
      padding: 12px 16px;
      border-radius: 20px;
      animation: fadeInUp 0.4s ease-out;
    }

    .user {
      background: #00adb5;
      align-self: flex-end;
    }

    .bot {
      background: #393e46;
      align-self: flex-start;
    }

    .input-area {
      display: flex;
      padding: 10px;
      border-top: 1px solid rgba(255, 255, 255, 0.1);
      background-color: rgba(0, 0, 0, 0.2);
    }

    .input-area input {
      flex: 1;
      padding: 10px 15px;
      border-radius: 20px;
      border: none;
      outline: none;
      font-size: 1em;
    }

    .input-area button {
      margin-left: 10px;
      padding: 10px 20px;
      border: none;
      border-radius: 20px;
      background: #00adb5;
      color: white;
      cursor: pointer;
      transition: background 0.3s ease;
    }

    .input-area button:hover {
      background: #019ca4;
    }

    @keyframes fadeInUp {
      0% {
        opacity: 0;
        transform: translateY(20px);
      }
      100% {
        opacity: 1;
        transform: translateY(0);
      }
    }

    .typing {
      display: inline-block;
      width: 50px;
      height: 20px;
    }

    .typing span {
      display: inline-block;
      width: 8px;
      height: 8px;
      margin: 0 2px;
      background: white;
      border-radius: 50%;
      animation: blink 1.2s infinite ease-in-out;
    }

    .typing span:nth-child(2) {
      animation-delay: 0.2s;
    }

    .typing span:nth-child(3) {
      animation-delay: 0.4s;
    }

    @keyframes blink {
      0%, 80%, 100% {
        transform: scale(0);
        opacity: 0.3;
      }
      40% {
        transform: scale(1);
        opacity: 1;
      }
    }
  </style>
</head>
<body>
  <div class="chat-container">
    <div class="messages" id="chat">
      <div class="message bot">Hi! I'm Vellure AI. How can I assist you today?</div>
    </div>
    <div class="input-area">
      <input type="text" id="input" placeholder="Type your message..." />
      <button onclick="sendMessage()">Send</button>
    </div>
  </div>

  <script>
    const chat = document.getElementById("chat");
    const input = document.getElementById("input");

    function sendMessage() {
      const text = input.value.trim();
      if (!text) return;

      addMessage("user", text);
      input.value = "";
      simulateBotResponse(text);
    }

    function addMessage(sender, text) {
      const msg = document.createElement("div");
      msg.className = `message ${sender}`;
      msg.textContent = text;
      chat.appendChild(msg);
      chat.scrollTop = chat.scrollHeight;
    }

    function simulateBotResponse(userInput) {
      const typing = document.createElement("div");
      typing.className = "message bot typing";
      typing.innerHTML = `<span></span><span></span><span></span>`;
      chat.appendChild(typing);
      chat.scrollTop = chat.scrollHeight;

      setTimeout(() => {
        typing.remove();
        addMessage("bot", "This is a simulated response to: " + userInput);
      }, 1500);
    }
  </script>
</body>
</html>
