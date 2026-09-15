# ✋ Finger-Count Quiz

A computer-basics quiz you play with your **webcam**, not your mouse. Instead of clicking an answer, you hold up the number of fingers that matches your choice — one finger for option 1, two for option 2, and so on — and the app locks in your answer automatically once it detects a stable gesture.

Everything runs **entirely in the browser**. No video is uploaded or stored anywhere.

## Demo

Open `gesture_quiz.html` in a browser, allow camera access, and start answering with your hand.

## Features

- 🖐️ **Real-time hand tracking** powered by [MediaPipe Hands](https://developers.google.com/mediapipe)
- 🔢 **Finger counting** using index, middle, ring, and pinky landmarks (thumb is ignored for reliability across hand orientations)
- ⏱️ **Stability check** — a gesture must hold steady for ~12 consecutive frames before it's accepted, preventing accidental misfires
- 📊 **Live progress bar, score tracker, and instant feedback** on each answer
- 🎨 **Clean dark UI** with a custom theme (Space Grotesk + Inter fonts)
- 🔁 **Replay support** — restart the quiz and try to beat your score
- 🔒 **Privacy-first** — all hand tracking happens locally on-device; no camera data ever leaves the browser

## How it works

1. Click **"Turn on camera & start"** and grant camera permission.
2. Read the question and its numbered options.
3. Hold up the matching number of fingers (1–4) in front of your camera.
4. Once the count is held steady, your answer is locked in automatically and marked correct/incorrect.
5. The quiz moves to the next question — repeat until you finish all questions and see your final score.

## Tech stack

| Component | Purpose |
|---|---|
| **MediaPipe Hands** | Hand landmark detection |
| **MediaPipe Camera Utils** | Webcam frame capture pipeline |
| **MediaPipe Drawing Utils** | Rendering hand skeleton overlay |
| Vanilla **HTML / CSS / JavaScript** | UI, quiz logic, game state |

No build tools, frameworks, or backend required — it's a single self-contained HTML file.

## Customizing the questions

All quiz content lives in one array near the top of the `<script>` section:

```js
const QUESTIONS = [
  { q: "What does CPU stand for?", options: ["Central Processing Unit", "Computer Personal Unit", "Central Program Utility", "Central Processor Unity"], answer: 0 },
  // add more questions here...
];
```

- `q`: the question text
- `options`: up to **4** answer choices (limited to 4 since fingers only go up to 4 on one hand)
- `answer`: the index (starting at 0) of the correct option

## Running locally

No installation needed — just open the HTML file in a modern browser (Chrome, Edge, or Firefox recommended for best `getUserMedia` and MediaPipe support).

```bash
# Optional: serve locally instead of opening the file directly
python3 -m http.server 8000
```

Then visit `http://localhost:8000/gesture_quiz.html`.

> **Note:** Some browsers restrict camera access on files opened directly via `file://`. If the camera doesn't start, try serving the file over `http://localhost` instead.

## Browser requirements

- A webcam
- A browser that supports `getUserMedia` (Chrome, Edge, Firefox, Safari 11+)
- Internet connection on first load (to fetch the MediaPipe libraries from CDN)

## License

Feel free to use, modify, and build on this project.
