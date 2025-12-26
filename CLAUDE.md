# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

neurotimer is a single-page web application (SPA) that implements a science-based study timer. The entire application is contained in `version3.html` - a self-contained HTML file with embedded CSS and JavaScript. There are no build tools, dependencies, or external libraries required.

## Architecture

### Single-File Structure

The application uses a monolithic architecture with three main sections in `version3.html`:

1. **CSS (lines 11-616)**: Japandi-inspired design system with custom properties for theming
2. **HTML (lines 618-778)**: Four main screen sections managed by visibility toggling
3. **JavaScript (lines 780-1450)**: Vanilla JS implementing the entire application logic

### State Management

The application uses a single global `state` object (line 782) that tracks:
- `currentStackIndex`: Current position in the card stack during onboarding
- `queue`: Array of study chunks to process during a session
- `currentIndex`: Current position in the study queue
- `examDate`: Optional exam date for spaced repetition calculations
- `stats`: Session statistics (time studied, breaks taken, etc.)
- `recalls`: User's elaborative interrogation responses

### Screen Flow

The application has four distinct screens controlled by `switchScreen()`:

1. **Onboarding** (`screen-onboarding`): Two-column layout with card stack navigation
   - Left: Subject/chunk input with visual card stack
   - Right: Sticky sidebar with session configuration

2. **Session** (`screen-session`): Timer display with phase management
   - Priming phase (2 min by default)
   - Deep work phase (customizable per chunk)
   - Break phase (5 min)

3. **Recall** (`screen-recall`): Elaborative interrogation prompt after each chunk

4. **Wrapup** (`screen-wrapup`): Session summary with progress ring visualization

### Key Components

**Card Stack System (lines 804-890)**
- Visual 3D stack navigation using CSS transforms
- Only the current card (index 0) is interactive
- Cards use `transform: translateY() scale() translateX()` for depth effect

**Timer System (lines 1380-1399)**
- Uses `setInterval` for countdown
- Tracks both study time and break time separately
- Updates progress bar based on elapsed time percentage

**Queue System (lines 1345-1371)**
- Modal overlay showing all study chunks
- Visual indicators for completed, current, and upcoming items
- Breadcrumb display in session header



## Development Workflow

### Running the Application

Simply open `version3.html` in a web browser:
```bash
open version3.html
```

No build process, server, or dependencies required.

### Testing Changes

Since this is a single HTML file:
1. Make edits to `version3.html`
2. Refresh the browser to see changes
3. Use browser DevTools for debugging

### Code Organization Guidelines

When modifying the codebase:

**CSS Sections:**
- Root variables (lines 12-25): Color palette and typography
- Utility classes (lines 64-65): `hidden` and `invisible` states
- Component-specific styles organized by feature

**JavaScript Organization:**
- State management at top (lines 782-802)
- Helper functions grouped by feature (stack, timer, queue, etc.)
- Event handlers reference functions by name (not inline)
- `DOMContentLoaded` initializer at bottom (lines 1415-1449)

**Important Patterns:**
- All screen transitions use `switchScreen(screenName)` function
- Timer always cleared with `clearInterval(timerInterval)` before starting new timer
- Phase changes trigger both UI updates and breathing circle state changes
- All controls hidden via `hideAllControls()` before showing relevant control group

## Cognitive Science Implementation

The application implements five key learning techniques:

1. **Interleaving**: Automatic subject switching within sessions
2. **Priming**: 2-minute preview phase before deep work
3. **Chunking**: User breaks subjects into bite-sized topics
4. **Elaborative Interrogation**: Post-study "why" questions
5. **Spaced Repetition**: Next review date calculation based on exam proximity

These are referenced in the README research section and should be preserved when making changes to the study flow.

## File Structure

```
.
├── README.md           # Project description and research references
├── version3.html       # Complete application (HTML/CSS/JS)
└── LICENSE            # MIT License
```

## Common Modifications

**Adjusting Default Timings:**
- Priming duration: Line 1166 (`startTimer(2 * 60, ...)`)
- Break duration: Line 1228 (`startTimer(5 * 60, ...)`)
- Extension time: Line 1209 (`startTimer(5 * 60, ...)`)

**Modifying Color Scheme:**
- Edit CSS custom properties in `:root` (lines 12-25)
- Colors follow Japandi aesthetic (warm, natural, minimal)

**Adding New Study Phases:**
- Create new control group in HTML
- Add phase transition function following `startChunkPhase()` pattern
- Update `hideAllControls()` to include new control group

**Changing Study Tips:**
- Edit `studyTips` array (lines 894-900)
- Tips rotate every 12 seconds (line 918)

## To-Do's

-**Fix onHover at Session Complete Screen**: Progress ring at Session Complete screen does not show minutes and seconds spent on each phase onHover. On mouseHover, each segment of the ring should show the respective stat that it represents (Example: Study 1min30sec, Break 0min1sec)