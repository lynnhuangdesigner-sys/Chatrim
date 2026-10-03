# Chatrim

**A smart chat-log stitcher for MMORPGs.** Drop in a pile of chat screenshots and get back one clean, correctly ordered long image, with player names hidden if you want them to be.

### 👉 [Try it in your browser](https://lynnhuangdesigner-sys.github.io/Chatrim/)

Everything runs locally. Your screenshots never leave your computer.

<!-- Add a preview image or GIF here (hide names first with "Hide names") -->
<!-- ![Chatrim preview](docs/preview.png) -->

---

## Why I made it

MMORPG players share chat logs all the time: a funny party moment, a roleplay scene, proof of what someone actually said. The usual process is painful. You take a dozen screenshots, they come out of order, half of each one is game UI, system spam is mixed in with the conversation, and everyone's character name is visible.

Chatrim handles all of that in one place.

## What it does

- **Finds the chat window on its own** and crops out the game UI, input box, and half-cut lines.
- **Sorts screenshots by their timestamps**, removes duplicate lines where screenshots overlap, and flags gaps where something might be missing.
- **Filters by channel.** Party, Tell, Say, and emotes stay; system messages and strangers' shouts go. Unknown colors become new channels automatically.
- **Hides names and timestamps** with mosaic or color blocks and aliases ("Player A", "Player B"). Names are matched by shape, so they're caught mid-sentence and even when split across a line break.
- **Lets you insert images** between any two messages, and edit everything directly on the canvas with undo and redo.
- **Turns the chat into text** with on-device OCR, keeping line breaks, bold names, and channel colors.
- **Works in English and Chinese**, switchable without losing your work.

There's also a plain Crop & Stitch mode for any screenshots that aren't chat logs.

## How it was made

I designed and directed Chatrim over four days (Sept 29 to Oct 2, 2026), building it with an AI coding assistant through 20+ reviewed iterations. My role was the product and design side: defining the problem, writing the spec, setting the scope of each round, testing every build against real screenshots, and deciding what to change, what to keep, and what to cut.

A few decisions that shaped it:

- **Editing moved onto the canvas.** An early side-panel list was removed because it was too narrow to read and pulled attention away from the actual content.
- **Two modes instead of one.** Mixing "messages" and "images" in one list confused the information architecture, so chat and crop became separate tools.
- **Test before building.** Two OCR engines were compared on real screenshots before any feature work. The first one garbled player names, so it was dropped.
- **Trust as a design problem.** The first OCR run downloads a model, which can look broken. A designed loading state now explains it, with progress and a time estimate.

The [Releases](../../releases) page walks through the project milestone by milestone.

## Tech notes

- A single HTML file with no build step and no backend
- Chat detection is plain pixel analysis: timestamps anchor each line, and text color identifies the channel
- Timestamp OCR with [tesseract.js](https://github.com/naptha/tesseract.js)
- Text recognition with [PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR) PP-OCRv4 models through [ONNX Runtime Web](https://github.com/microsoft/onnxruntime), running in a Web Worker so the page stays responsive
- Models download once from jsDelivr and are cached by the browser

## Run it locally

Download `index.html` from the latest release and open it in Chrome, Edge, or Firefox. Timestamp sorting and image to text need an internet connection the first time, to download their models.

## Credits

Text recognition uses these open-source projects: PaddleOCR (Apache-2.0), ONNX Runtime Web (MIT), tesseract.js (Apache-2.0), and the PP-OCRv4 ONNX models packaged in [@gutenye/ocr-models](https://www.npmjs.com/package/@gutenye/ocr-models).

## About

Designed by **Lynn Huang**. Released under the [MIT License](LICENSE).

<sub>Chatrim is an unofficial fan-made tool and is not affiliated with any game publisher.</sub>
