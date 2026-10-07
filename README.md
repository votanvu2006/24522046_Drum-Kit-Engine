# Drum Kit Engine

A contract-first Drum Kit Engine built with Vanilla HTML5, modern CSS, and ES6+ JavaScript.

## Project Overview

This project implements a keyboard-controlled drum kit with an independently designed audio playback engine and FIFO beat recorder.

The architecture follows a contract-first approach where the HTML defines the audio and keyboard mapping contract, while JavaScript handles playback, keyboard events, and beat recording independently.

## Technologies

* HTML5
* Modern CSS
* JavaScript ES6+
* Git & GitHub
* Live Server

## Architecture

The project separates the main responsibilities into independent components:

```text
HTML Contract
    │
    ├── data-key
    └── data-sound
          │
          ▼
    Audio Engine
          │
          ▼
     Audio Playback

Keyboard Events
    │
    ├── keydown
    ├── event.key
    └── event.repeat
          │
          ▼
       Trigger
       ├── Audio Engine
       └── Beat Recorder
              │
              ▼
          FIFO Queue
```

## Features

* Keyboard-controlled drum pads
* Clickable drum pads
* Polyphonic audio playback
* `data-sound` HTML audio contract
* `keydown` keyboard handling
* `event.repeat` throttling
* Timestamped FIFO beat recording
* Responsive CSS Grid layout
* Semantic HTML structure
* Keyboard-accessible controls

## Project Structure

```text
24522046_Drum-Kit-Engine/
│
├── assets/
│   └── audio/
│
├── TASK_DECOMPOSITION.md
├── index.html
├── styles.css
├── audio-engine.js
├── recorder.js
├── app.js
└── README.md
```

## Architectural Requirements

### HTML Audio Contract

Each drum pad defines its keyboard mapping and audio source through HTML data attributes:

```html
<button
    class="drum-pad"
    data-key="a"
    data-sound="assets/audio/kick.wav"
>
    A
</button>
```

The JavaScript audio engine reads the audio source from the HTML contract instead of hard-coding individual audio paths.

### Audio Engine

The audio engine is independent from keyboard event handling.

Each triggered sound creates an independent `Audio` instance, allowing multiple sounds to play without replacing an already active sound.

### Keyboard Handling

Keyboard interaction uses:

* `keydown`
* `event.key`
* `event.repeat`

Repeated `keydown` events caused by holding a key are ignored to prevent repeated audio triggering.

### Beat Recorder

The Beat Recorder stores timestamped keyboard events in FIFO order.

Each recorded event contains:

* Key
* Timestamp

## Development Workflow

The project follows atomic Git commits instead of a single monolithic commit.

Required commit sequence:

```text
docs(spec): define component contracts & WBS table
feat(html): build semantic landmark tree (zero divs)
feat(css): implement design tokens & box-sizing reset
feat(css): build 2D responsive grid layout
feat(js): implement decoupled audio engine logic
feat(js): bind keydown events with repeat throttling
```

## Verification

The implementation should verify:

* Audio sources can be changed through `data-sound` without rewriting the audio engine.
* Multiple drum sounds can play independently.
* Holding a keyboard key does not repeatedly trigger the sound.
* Beat events preserve FIFO order.
* The interface remains usable on a 375px viewport.
* The implementation uses Vanilla HTML5, modern CSS, and ES6+ JavaScript without external frameworks or script CDNs.

## Running the Project

Run the project using a local development server such as VS Code Live Server.

Do not open the project directly using:

```text
file:///...
```

## Academic Context

This project is developed as part of the Web Application Development Lab 1 — HW2: Drum Kit Engine (Contract-First).
