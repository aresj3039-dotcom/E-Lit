<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="theme-color" content="#f5f7fb">
  <title>Random Text Generator</title>
  <style>
    :root {
      color-scheme: light;
      font-family: Inter, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
      color: #172033;
      background: #f5f7fb;
      font-synthesis: none;
      text-rendering: optimizeLegibility;
    }

    * {
      box-sizing: border-box;
    }

    body {
      min-width: 320px;
      min-height: 100vh;
      margin: 0;
      padding: 48px 20px;
      background:
        radial-gradient(ellipse at 12% 0%, rgba(196, 213, 255, 0.48), transparent 34rem),
        #f5f7fb;
    }

    button,
    select,
    input,
    textarea {
      font: inherit;
    }

    .container {
      width: min(100%, 760px);
      margin: 0 auto;
    }

    .intro {
      margin: 0 0 28px;
      text-align: center;
    }

    .eyebrow {
      margin: 0 0 10px;
      color: #4d63d8;
      font-size: 0.76rem;
      font-weight: 750;
      letter-spacing: 0.13em;
      text-transform: uppercase;
    }

    h1 {
      margin: 0;
      font-size: clamp(2rem, 6vw, 3rem);
      letter-spacing: -0.055em;
      line-height: 1.1;
    }

    .subtitle {
      margin: 14px 0 0;
      color: #64708a;
      font-size: 1.02rem;
      line-height: 1.6;
    }

    .card {
      padding: clamp(22px, 5vw, 36px);
      border: 1px solid #e5e9f2;
      border-radius: 22px;
      background: rgba(255, 255, 255, 0.94);
      box-shadow: 0 22px 60px rgba(37, 52, 94, 0.09);
    }

    .controls {
      display: grid;
      grid-template-columns: minmax(0, 1fr) minmax(110px, 0.62fr) auto;
      gap: 16px;
      align-items: end;
      padding-bottom: 26px;
      border-bottom: 1px solid #edf0f6;
    }

    .field {
      display: grid;
      gap: 8px;
    }

    label {
      color: #35415a;
      font-size: 0.88rem;
      font-weight: 700;
    }

    select,
    input {
      width: 100%;
      min-height: 48px;
      padding: 0 13px;
      border: 1px solid #dce2ed;
      border-radius: 10px;
      outline: none;
      background: #fff;
      color: #172033;
    }

    select:focus-visible,
    input:focus-visible,
    textarea:focus-visible,
    button:focus-visible {
      outline: 3px solid #bac6ff;
      outline-offset: 2px;
    }

    button {
      min-height: 48px;
      padding: 0 19px;
      border: 0;
      border-radius: 10px;
      background: #4d63d8;
      color: #fff;
      font-weight: 700;
      cursor: pointer;
      transition: background 150ms ease, transform 150ms ease;
    }

    button:hover {
      background: #3e53c3;
    }

    button:active {
      transform: translateY(1px);
    }

    .output-heading {
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 16px;
      margin: 24px 0 12px;
    }

    .word-workspace {
      display: none;
      gap: 18px;
      margin: 20px 0;
    }

    .word-workspace.is-visible {
      display: grid;
    }

    .word-area {
      min-width: 0;
    }

    .word-area-heading {
      display: flex;
      align-items: baseline;
      justify-content: space-between;
      gap: 12px;
      margin-bottom: 9px;
    }

    .word-area-heading h3 {
      margin: 0;
      color: #35415a;
      font-size: 0.88rem;
    }

    .word-hint {
      margin: 0;
      color: #758098;
      font-size: 0.78rem;
    }

    .word-tray,
    .poem-canvas {
      display: flex;
      flex-wrap: wrap;
      align-content: flex-start;
      gap: 8px;
      min-height: 74px;
      padding: 12px;
      border: 1px solid #e1e6ef;
      border-radius: 12px;
      background: #fafbfe;
    }

    .word-tile {
      min-height: 36px;
      padding: 0 12px;
      border: 1px solid #dce2ed;
      border-radius: 999px;
      background: #fff;
      color: #35415a;
      font-size: 0.88rem;
      font-weight: 600;
      cursor: grab;
    }

    .word-tile:hover {
      border-color: #9aa8ed;
      background: #f3f5ff;
    }

    .word-tile:active,
    .poem-token[draggable="true"] {
      cursor: grab;
    }

    .poem-canvas {
      min-height: 100px;
      align-items: center;
      border-style: dashed;
      background: #fff;
    }

    .poem-canvas.is-over,
    .word-tray.is-over {
      border-color: #7185e8;
      background: #f3f5ff;
    }

    .poem-token {
      display: inline-flex;
      align-items: center;
      gap: 2px;
      padding: 3px 4px 3px 11px;
      border: 1px solid #dce2ed;
      border-radius: 999px;
      background: #fff;
      color: #35415a;
      font-size: 0.88rem;
      font-weight: 600;
    }

    .token-action {
      display: inline-grid;
      width: 26px;
      min-height: 26px;
      padding: 0;
      place-items: center;
      border-radius: 50%;
      background: transparent;
      color: #64708a;
      font-size: 0.85rem;
      line-height: 1;
    }

    .token-action:hover {
      background: #edf0f7;
      color: #172033;
    }

    .token-action:disabled {
      cursor: default;
      opacity: 0.35;
    }

    .poem-empty {
      width: 100%;
      margin: 0;
      color: #96a0b3;
      font-size: 0.88rem;
      text-align: center;
    }

    h2 {
      margin: 0;
      font-size: 1rem;
      letter-spacing: -0.01em;
    }

    .copy-button {
      min-height: 38px;
      padding: 0 13px;
      border: 1px solid #dce2ed;
      background: #fff;
      color: #35415a;
      font-size: 0.85rem;
    }

    .copy-button:hover {
      background: #f4f6fb;
    }

    textarea {
      display: block;
      width: 100%;
      min-height: 250px;
      padding: 17px;
      resize: vertical;
      border: 1px solid #e1e6ef;
      border-radius: 12px;
      outline: none;
      background: #fafbfe;
      color: #263149;
      line-height: 1.75;
    }

    textarea.output-hidden {
      display: none;
    }

    textarea::placeholder {
      color: #96a0b3;
    }

    .status-row {
      display: flex;
      justify-content: space-between;
      gap: 16px;
      min-height: 24px;
      margin-top: 10px;
      color: #758098;
      font-size: 0.82rem;
    }

    #status {
      margin: 0;
    }

    #status[data-error="true"] {
      color: #b42318;
    }

    @media (max-width: 600px) {
      body {
        padding: 30px 14px;
      }

      .controls {
        grid-template-columns: 1fr 1fr;
      }

      .generate-button {
        grid-column: 1 / -1;
      }

      .status-row {
        flex-direction: column;
        gap: 4px;
      }
    }

    @media (prefers-reduced-motion: reduce) {
      *,
      *::before,
      *::after {
        scroll-behavior: auto !important;
        transition-duration: 0.01ms !important;
      }
    }
  </style>
  <script defer>
    document.addEventListener("DOMContentLoaded", () => {
    const wordBank = [
      "bright", "river", "garden", "quiet", "journey",
      "silver", "forest", "morning", "window", "curious",
      "cloud", "gentle", "planet", "music", "future",
      "hidden", "ocean", "lantern", "wonder", "meadow",
      "creative", "sunlight", "path", "dream", "stone",
      "whisper", "colorful", "adventure", "breeze", "story",
      "beautiful", "explore", "peaceful", "mountain", "discovery",
      "imagine", "village", "energy", "mystery", "freedom"
    ];

    const textType = document.getElementById("textType");
    const amountInput = document.getElementById("amount");
    const output = document.getElementById("output");
    const status = document.getElementById("status");
    const wordCount = document.getElementById("wordCount");
    const generateBtn = document.getElementById("generateBtn");
    const copyBtn = document.getElementById("copyBtn");
    const wordWorkspace = document.getElementById("wordWorkspace");
    const wordTray = document.getElementById("wordTray");
    const poemCanvas = document.getElementById("poemCanvas");
    const outputHeading = document.getElementById("outputHeading");
    let availableWords = [];
    let poemWords = [];
    let nextWordId = 0;

    // Return one random word.
    function randomWord() {
      const index = Math.floor(Math.random() * wordBank.length);
      return wordBank[index];
    }

    // Generate a sentence with random words.
    function generateSentence() {
      const length = Math.floor(Math.random() * 8) + 6;
      const words = [];

      for (let i = 0; i < length; i++) {
        words.push(randomWord());
      }

      const sentence = words.join(" ");
      return sentence.charAt(0).toUpperCase() +
        sentence.slice(1) + ".";
    }

    // Generate one paragraph containing three sentences.
    function generateParagraph() {
      const sentences = [];

      for (let i = 0; i < 3; i++) {
        sentences.push(generateSentence());
      }

      return sentences.join(" ");
    }

    function updateWordCount() {
      const count = output.value.trim()
        ? output.value.trim().split(/\s+/).length
        : 0;
      wordCount.textContent = `${count} ${count === 1 ? "word" : "words"}`;
    }

    function updatePoemOutput() {
      output.value = poemWords.map(({ word }) => word).join(" ");
      updateWordCount();
    }

    function addWord(token, index = poemWords.length) {
      poemWords.splice(index, 0, { id: nextWordId++, word: token.word });
      renderPoem();
    }

    function renderWordTray() {
      wordTray.replaceChildren();

      availableWords.forEach((token) => {
        const button = document.createElement("button");
        button.type = "button";
        button.className = "word-tile";
        button.textContent = token.word;
        button.draggable = true;
        button.setAttribute("aria-label", `Add ${token.word} to your poem or story`);
        button.addEventListener("click", () => addWord(token));
        button.addEventListener("dragstart", (event) => {
          event.dataTransfer.setData("text/plain", JSON.stringify({
            source: "tray",
            id: token.id
          }));
          event.dataTransfer.effectAllowed = "copy";
        });
        wordTray.append(button);
      });
    }

    function movePoemWord(from, to) {
      if (to < 0 || to >= poemWords.length) return;
      const [token] = poemWords.splice(from, 1);
      poemWords.splice(to, 0, token);
      renderPoem();
    }

    function renderPoem() {
      poemCanvas.replaceChildren();

      if (poemWords.length === 0) {
        const emptyMessage = document.createElement("p");
        emptyMessage.className = "poem-empty";
        emptyMessage.textContent = "Drop words here or click words in the tray to begin.";
        poemCanvas.append(emptyMessage);
      }

      poemWords.forEach((token, index) => {
        const item = document.createElement("span");
        item.className = "poem-token";
        item.draggable = true;
        item.setAttribute("role", "listitem");
        item.setAttribute("aria-label", `${token.word}, position ${index + 1}`);
        item.addEventListener("dragstart", (event) => {
          event.dataTransfer.setData("text/plain", JSON.stringify({
            source: "poem",
            id: token.id
          }));
          event.dataTransfer.effectAllowed = "move";
        });
        item.addEventListener("dragover", (event) => event.preventDefault());
        item.addEventListener("drop", (event) => handleWordDrop(event, index));

        const word = document.createElement("span");
        word.textContent = token.word;
        item.append(word);

        const moveLeft = document.createElement("button");
        moveLeft.type = "button";
        moveLeft.className = "token-action";
        moveLeft.textContent = "←";
        moveLeft.setAttribute("aria-label", `Move ${token.word} left`);
        moveLeft.disabled = index === 0;
        moveLeft.addEventListener("click", () => movePoemWord(index, index - 1));
        item.append(moveLeft);

        const moveRight = document.createElement("button");
        moveRight.type = "button";
        moveRight.className = "token-action";
        moveRight.textContent = "→";
        moveRight.setAttribute("aria-label", `Move ${token.word} right`);
        moveRight.disabled = index === poemWords.length - 1;
        moveRight.addEventListener("click", () => movePoemWord(index, index + 1));
        item.append(moveRight);

        const remove = document.createElement("button");
        remove.type = "button";
        remove.className = "token-action";
        remove.textContent = "×";
        remove.setAttribute("aria-label", `Remove ${token.word}`);
        remove.addEventListener("click", () => {
          poemWords.splice(index, 1);
          renderPoem();
        });
        item.append(remove);
        poemCanvas.append(item);
      });

      updatePoemOutput();
    }

    function handleWordDrop(event, insertAt = poemWords.length) {
      event.preventDefault();
      event.stopPropagation();
      poemCanvas.classList.remove("is-over");

      let payload;
      try {
        payload = JSON.parse(event.dataTransfer.getData("text/plain"));
      } catch {
        return;
      }

      if (payload.source === "tray") {
        const token = availableWords.find((word) => word.id === payload.id);
        if (token) addWord(token, insertAt);
      } else if (payload.source === "poem") {
        const from = poemWords.findIndex((word) => word.id === payload.id);
        if (from === -1) return;
        const [token] = poemWords.splice(from, 1);
        const adjustedIndex = from < insertAt ? insertAt - 1 : insertAt;
        poemWords.splice(adjustedIndex, 0, token);
        renderPoem();
      }
    }

    // Main generator function.
    function generateText() {
      const type = textType.value;
      const amount = Number(amountInput.value);
      status.textContent = "";
      status.dataset.error = "false";

      if (
        !Number.isInteger(amount) ||
        amount < 1 ||
        amount > 100
      ) {
        status.textContent = "Enter a whole number from 1 to 100.";
        status.dataset.error = "true";
        return;
      }

      const isWords = type === "words";
      wordWorkspace.classList.toggle("is-visible", isWords);
      output.classList.toggle("output-hidden", isWords);
      outputHeading.textContent = isWords ? "Your text" : "Generated text";

      let result = [];

      if (type === "words") {
        availableWords = Array.from({ length: amount }, () => ({
          id: nextWordId++,
          word: randomWord()
        }));
        poemWords = [];
        renderWordTray();
        renderPoem();
      } else if (type === "sentences") {
        for (let i = 0; i < amount; i++) {
          result.push(generateSentence());
        }

        output.value = result.join(" ");
      } else if (type === "paragraphs") {
        for (let i = 0; i < amount; i++) {
          result.push(generateParagraph());
        }

        output.value = result.join("\n\n");
      }

      if (!isWords) updateWordCount();
      status.textContent = "Text generated successfully.";
    }

    // Copy the generated text.
    async function copyText() {
      if (!output.value.trim()) {
        status.textContent = "Generate some text first.";
        status.dataset.error = "true";
        return;
      }

      try {
        await navigator.clipboard.writeText(output.value);
      } catch {
        // Fallback for browsers where clipboard access is blocked.
        output.select();
        const copied = document.execCommand("copy");

        status.textContent = copied
          ? "Text copied to clipboard!"
          : "Copy failed. Select the text and copy it manually.";
        status.dataset.error = copied ? "false" : "true";
        return;
      }

      status.textContent = "Text copied to clipboard!";
      status.dataset.error = "false";
    }

    generateBtn.addEventListener("click", generateText);
    copyBtn.addEventListener("click", copyText);
    output.addEventListener("input", updateWordCount);
    poemCanvas.addEventListener("dragover", (event) => {
      event.preventDefault();
      poemCanvas.classList.add("is-over");
    });
    poemCanvas.addEventListener("dragleave", (event) => {
      if (!poemCanvas.contains(event.relatedTarget)) {
        poemCanvas.classList.remove("is-over");
      }
    });
    poemCanvas.addEventListener("drop", handleWordDrop);
    wordTray.addEventListener("dragover", (event) => {
      event.preventDefault();
      wordTray.classList.add("is-over");
    });
    wordTray.addEventListener("dragleave", () => wordTray.classList.remove("is-over"));
    wordTray.addEventListener("drop", (event) => {
      event.preventDefault();
      wordTray.classList.remove("is-over");
      let payload;
      try {
        payload = JSON.parse(event.dataTransfer.getData("text/plain"));
      } catch {
        return;
      }

      if (payload.source !== "poem") return;
      const index = poemWords.findIndex((word) => word.id === payload.id);
      if (index !== -1) {
        poemWords.splice(index, 1);
        renderPoem();
      }
    });
    // Generate an initial example when the page loads.
    amountInput.addEventListener("keydown", (event) => {
      if (event.key === "Enter") generateText();
    });

    generateText();
    });
  </script>
</head>
<body>
  <main class="container">
    <header class="intro">
      <p class="eyebrow">A little inspiration</p>
      <h1>Random Text Generator</h1>
      <p class="subtitle">Create a few words, a sentence, or a whole paragraph in a click.</p>
    </header>

    <section class="card" aria-label="Text generator">
      <div class="controls">
        <div class="field">
          <label for="textType">Text type</label>
          <select id="textType">
            <option value="words">Words</option>
            <option value="sentences">Sentences</option>
            <option value="paragraphs">Paragraphs</option>
          </select>
        </div>

        <div class="field">
          <label for="amount">Amount</label>
          <input id="amount" type="number" min="1" max="100" value="3">
        </div>

        <button id="generateBtn" class="generate-button" type="button">Generate text</button>
      </div>

      <div class="output-heading">
        <h2 id="outputHeading">Generated text</h2>
        <button id="copyBtn" class="copy-button" type="button">Copy text</button>
      </div>

      <section id="wordWorkspace" class="word-workspace" aria-label="Build a poem or story">
        <div class="word-area">
          <div class="word-area-heading">
            <h3>Word tray</h3>
            <p class="word-hint">Drag or click a word to add it</p>
          </div>
          <div id="wordTray" class="word-tray" aria-label="Available words"></div>
        </div>
        <div class="word-area">
          <div class="word-area-heading">
            <h3>Your poem or story</h3>
            <p class="word-hint">Drag to rearrange; use arrows to move</p>
          </div>
          <div
            id="poemCanvas"
            class="poem-canvas"
            role="list"
            aria-label="Your poem or story. Drop words here."
          ></div>
        </div>
      </section>

      <textarea
        id="output"
        aria-labelledby="outputHeading"
        placeholder="Your generated text will appear here..."
        spellcheck="false"
      ></textarea>

      <div class="status-row">
        <p id="status" role="status" aria-live="polite"></p>
        <span id="wordCount" aria-live="polite">0 words</span>
      </div>
    </section>
  </main>
</body>
</html>
