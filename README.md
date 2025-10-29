# Text-to-Speech-TTS-Tool

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Text to Speech Tool</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 40px;
      background: #fafafa;
      color: #333;
    }
    textarea {
      width: 100%;
      height: 150px;
      padding: 10px;
      font-size: 16px;
      border: 1px solid #ccc;
      border-radius: 5px;
      resize: none;
    }
    button {
      margin: 10px 5px 0 0;
      padding: 10px 16px;
      font-size: 15px;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      background-color: #007bff;
      color: white;
      transition: 0.3s;
    }
    button:hover {
      background-color: #0056b3;
    }
    select {
      padding: 5px;
      margin-top: 10px;
      font-size: 15px;
    }
  </style>
</head>
<body>
  <h2>Text to Speech Tool</h2>
  <textarea id="text" placeholder="Type or paste your text here..."></textarea>
  <br>
  <select id="voiceSelect"></select>
  <br>
  <button onclick="speakText()">🔊 Speak</button>
  <button onclick="stopSpeaking()">⏹ Stop</button>

  <script>
    const textArea = document.getElementById('text');
    const voiceSelect = document.getElementById('voiceSelect');
    let voices = [];

    function loadVoices() {
      voices = speechSynthesis.getVoices();
      voiceSelect.innerHTML = '';
      voices.forEach((voice, i) => {
        const option = document.createElement('option');
        option.value = i;
        option.textContent = `${voice.name} (${voice.lang})`;
        voiceSelect.appendChild(option);
      });
    }

    loadVoices();
    speechSynthesis.onvoiceschanged = loadVoices;

    function speakText() {
      const text = textArea.value.trim();
      if (text === '') return alert('Please enter some text to speak.');
      const utterance = new SpeechSynthesisUtterance(text);
      utterance.voice = voices[voiceSelect.value];
      speechSynthesis.speak(utterance);
    }

    function stopSpeaking() {
      speechSynthesis.cancel();
    }
  </script>
</body>
</html>
