# GEMINI.md

This file provides context for Gemini when working with the `neurotimer` repository.

## Project Overview

`neurotimer` is a single-page web application (SPA) designed as a science-based study timer. It operationalizes cognitive science principles like interleaving, priming, and spaced repetition into a unified interface.

The entire application is self-contained within a single file: `version3.html`.

## Architecture & Tech Stack

*   **Type**: Static HTML/CSS/JS (Monolith)
*   **Main File**: `version3.html`
*   **Dependencies**: None (Vanilla JS, embedded CSS).
*   **Fonts**: Fetched from Google Fonts (DM Sans, Inter).

### Code Structure (`version3.html`)

The file is organized into three distinct sections:
1.  **CSS (Style)**: Located in the `<style>` block. Uses CSS custom properties (variables) for theming (Japandi palette).
2.  **HTML (Structure)**: Contains four main screen sections, whose visibility is toggled via JavaScript.
3.  **JavaScript (Logic)**: Located in the `<script>` block at the bottom. Handles state, DOM manipulation, and timer logic.

### State Management

Global state is managed via a `state` object in the JavaScript section, tracking:
*   `currentStackIndex`: Onboarding card position.
*   `queue`: The list of study chunks.
*   `currentIndex`: Current active chunk.
*   `stats`: Session metrics.

### Key Workflows

*   **Screen Switching**: The `switchScreen(screenName)` function manages navigation between:
    *   `screen-onboarding`: Initial setup and chunk entry.
    *   `screen-session`: The main timer interface (Priming -> Deep Work -> Break).
    *   `screen-recall`: Post-chunk "Why" questions (Elaborative Interrogation).
    *   `screen-wrapup`: Final session summary.

## Development Workflow

### Running the Application
Since there is no build step, you can run the application by simply opening the file in a web browser.

```bash
# MacOS
open version3.html

# Linux
xdg-open version3.html

# Windows
start version3.html
```

### Making Changes
1.  **Edit**: Modify `version3.html` directly.
2.  **Verify**: Refresh the browser to see changes.
3.  **Debug**: Use standard browser Developer Tools.

## Development Conventions

*   **CSS**: Use the defined root variables (e.g., `--bg-color`, `--accent`) to maintain the design system.
*   **JS**: Keep helper functions grouped by feature (stack, timer, queue).
*   **Naming**: Follow the existing camelCase convention for functions and variables.
*   **Architecture**: Do not split the file into separate `.css` or `.js` files unless explicitly requested for a refactor. The single-file structure is intentional for portability.

## Cognitive Science Principles

The code implements specific logic to support:
*   **Interleaving**: Switching subjects automatically.
*   **Priming**: A dedicated 2-minute pre-study phase.
*   **Chunking**: Breaking inputs into manageable tasks.
*   **Elaborative Interrogation**: Prompting "Why?" questions after study blocks.
