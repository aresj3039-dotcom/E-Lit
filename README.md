<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>The Unsent Voicemail</title>
<style>
  :root { --bg: #14161a; --fg: #e8e4da; --accent: #d9a65a; --dim: #7c7a73; }
  * { box-sizing: border-box; }
  body {
    margin: 0; min-height: 100vh; background: var(--bg); color: var(--fg);
    font-family: Georgia, "Times New Roman", serif; line-height: 1.7;
    display: flex; justify-content: center; padding: 8vh 20px;
  }
  main { max-width: 36rem; width: 100%; }
  h1 { font-size: 0.85rem; letter-spacing: 0.3em; text-transform: uppercase;
       color: var(--dim); font-weight: normal; margin: 0 0 2.5rem; }
  #text p { margin: 0 0 1.2rem; font-size: 1.15rem; opacity: 0;
            animation: rise 1.2s ease forwards; }
  #text p:nth-child(2) { animation-delay: 0.6s; }
  #text p:nth-child(3) { animation-delay: 1.2s; }
  #text p:nth-child(4) { animation-delay: 1.8s; }
  @keyframes rise { from { opacity: 0; transform: translateY(6px); }
                    to   { opacity: 1; transform: none; } }
  #links { margin-top: 2rem; display: flex; flex-direction: column; gap: 0.6rem; }
  button.link {
    background: none; border: none; color: var(--accent); font: inherit;
    font-size: 1.05rem; text-align: left; padding: 0; cursor: pointer;
    opacity: 0; animation: rise 1s ease forwards; animation-delay: 2.4s;
  }
  button.link:hover, button.link:focus-visible { text-decoration: underline; outline: none; }
  .faded { color: var(--dim); }
  footer { margin-top: 4rem; font-size: 0.8rem; color: var(--dim); }
  footer button { background: none; border: none; color: var(--dim);
                  font: inherit; text-decoration: underline; cursor: pointer; padding: 0; }
</style>
</head>
<body>
<main>
  <h1>The Unsent Voicemail</h1>
  <div id="text" aria-live="polite"></div>
  <div id="links"></div>
  <footer><button id="restart">begin again</button></footer>
</main>

<script>
/* ============================================================
   EDIT THIS SECTION TO WRITE YOUR OWN STORY
   ------------------------------------------------------------
   Each passage has:
     text   - array of paragraphs (strings)
     again  - (optional) paragraphs shown when the reader returns
              to this passage a second time or later
     links  - array of { label, to, needs? }
              needs: (optional) a function(state) that must return
              true for the link to appear
     onEnter- (optional) function(state) that changes the state
   `state.memory` starts at 5 and shrinks as the reader revisits
   things; the story uses it to make the narrator's memory fade.
   ============================================================ */
const passages = {
  start: {
    text: [
      "Your phone buzzes: storage almost full. You start deleting old voicemails.",
      "Forty-one of them are spam. One is from your grandmother, dated three winters ago.",
      "Duration: 0:47. You never listened to it."
    ],
    links: [
      { label: "Play it", to: "play" },
      { label: "Delete it", to: "delete" },
      { label: "Put the phone down", to: "kitchen" }
    ]
  },

  play: {
    text: [
      "Static, then a kettle clicking off somewhere behind her voice.",
      "\"It's nothing important. I just wanted to hear if you were still the kind of person who picks up.\"",
      "A pause. The kettle again. Then the message ends."
    ],
    again: [
      "Static, then a kettle. Her voice is farther away than before.",
      "\"It's nothing important. I just wanted to hear if you were still...\"",
      "You can't remember how the sentence ends."
    ],
    onEnter: s => { s.heard = true; s.memory -= 1; },
    links: [
      { label: "Call her back", to: "call" },
      { label: "Play it again", to: "play" },
      { label: "Think about the last time you did pick up", to: "kitchen" }
    ]
  },

  delete: {
    text: [
      "Your thumb hovers. The red button is very small.",
      "You press it. The phone makes the soft sound of something going into a drawer.",
      "Thirty-nine voicemails left. Then forty. Then you lose count."
    ],
    onEnter: s => { s.deleted = true; s.memory -= 2; },
    links: [
      { label: "Try to remember what she said", to: "remember" },
      { label: "Put the phone down", to: "kitchen" }
    ]
  },

  kitchen: {
    text: [
      "You put the phone face-down on the counter and fill the kettle.",
      "While it heats, you notice the sound it makes. You know that sound. You have always known that sound."
    ],
    again: [
      "You fill the kettle again. The sound is just a sound now."
    ],
    onEnter: s => { s.memory -= 1; },
    links: [
      { label: "Pick the phone back up", to: "start" },
      { label: "Listen to the kettle", to: "remember", needs: s => !s.deleted },
      { label: "Try to remember her voice", to: "remember", needs: s => s.deleted }
    ]
  },

  call: {
    text: [
      "It rings four times.",
      "A recorded voice that isn't hers says the number you have dialed is no longer in service.",
      "You stay on the line a moment anyway, the way you might stand in a room after the light's been turned off."
    ],
    onEnter: s => { s.memory -= 1; },
    links: [
      { label: "Hang up", to: "end" }
    ]
  },

  remember: {
    text: [
      "You close your eyes and reach for it.",
      "Something about a kettle. Something about picking up."
    ],
    links: [
      { label: "Keep reaching", to: "end" }
    ]
  },

  end: {
    /* The ending text depends on the state, so it's a function. */
    dynamic: s => {
      if (s.heard && !s.deleted) {
        return {
          text: [
            "You have her voice, and the sentence, and the kettle.",
            "It isn't much. You save the voicemail, and for the first time in three winters, you let it stay."
          ]
        };
      }
      if (s.deleted) {
        return {
          text: [
            "There was a voice. There was a kettle. There was a question you were supposed to answer.",
            "<span class='faded'>You are almost sure of this.</span>"
          ]
        };
      }
      return {
        text: [
          "You never learn what she said.",
          "The phone sits on the counter, forty-one voicemails fewer, or one. You can't tell which."
        ]
      };
    },
    links: []
  }
};
/* ============================================================
   END OF EDITABLE SECTION. The engine below usually doesn't
   need changes unless you want new effects.
   ============================================================ */

const textEl = document.getElementById("text");
const linksEl = document.getElementById("links");
let state, visits;

function reset() {
  state = { memory: 5, heard: false, deleted: false };
  visits = {};
  go("start");
}

/* The "fade" effect: as state.memory drops, a growing share of
   words in the text are replaced with dots, so the narrator's
   memory visibly degrades as the reader moves through the story. */
function decay(str) {
  if (state.memory >= 4) return str;
  const chance = (4 - Math.max(state.memory, 0)) * 0.07;
  return str.replace(/>([^<]+)</g, (m, inner) => ">" + inner + "<")
            .split(/(\s+)/)
            .map(w => (/^\s+$/.test(w) || w.includes("<") || w.includes(">") || w.length < 5)
              ? w
              : (Math.random() < chance ? "·".repeat(w.length) : w))
            .join("");
}

function go(id) {
  const base = passages[id];
  visits[id] = (visits[id] || 0) + 1;
  if (base.onEnter) base.onEnter(state);

  const p = base.dynamic ? { ...base, ...base.dynamic(state) } : base;
  const paragraphs = (visits[id] > 1 && p.again) ? p.again : p.text;

  textEl.innerHTML = "";
  paragraphs.forEach(t => {
    const el = document.createElement("p");
    el.innerHTML = decay(t);
    textEl.appendChild(el);
  });

  linksEl.innerHTML = "";
  (p.links || [])
    .filter(l => !l.needs || l.needs(state))
    .forEach(l => {
      const b = document.createElement("button");
      b.className = "link";
      b.textContent = l.label;
      b.onclick = () => go(l.to);
      linksEl.appendChild(b);
    });
}

document.getElementById("restart").onclick = reset;
reset();
</script>
</body>
</html>
