# Stopwatch

A simple, accurate stopwatch built with plain **HTML, CSS, and JavaScript**. No frameworks, no libraries, no build tools. Just open `index.html` in your browser.

## Features

- Start, Stop, and Reset buttons
- Resume from where you stopped
- Time display in `HH:MM:SS.cc` format (hours, minutes, seconds, centiseconds)
- Accurate timing using `Date.now()`, so it stays correct even if the browser delays a tick or the tab is in the background
- Protection against duplicate timers (clicking Start many times does not speed it up)
- Clean, centered card design with color-coded buttons

## Technologies Used

| Technology | Purpose |
|---|---|
| HTML5 | Page structure |
| CSS3 | Layout and styling |
| JavaScript (ES6) | Stopwatch logic |

## Project Structure

```
stopwatch/
├── index.html   # Page structure
├── style.css    # Styling
├── script.js    # Stopwatch logic
└── README.md    # Project documentation
```

## Getting Started

### Run locally

1. Download or clone this repository:
   ```bash
   git clone https://github.com/your-username/stopwatch.git
   ```
2. Open the project folder:
   ```bash
   cd stopwatch
   ```
3. Open `index.html` in any modern browser (double-click it, or use a tool like VS Code Live Server).

No installation or setup is needed.

## How to Use

| Button | What it does |
|---|---|
| **Start** | Starts the stopwatch, or resumes it after a stop |
| **Stop** | Pauses the stopwatch and keeps the current time |
| **Reset** | Stops the stopwatch and sets the time back to `00:00:00.00` |

## How It Works

1. **State variables** outside the functions remember the stopwatch's status:
   - `timerId` stores the ID returned by `setInterval`, so the timer can be stopped later.
   - `startTime` stores the moment the timer started.
   - `elapsed` stores the total milliseconds passed.
2. **Start** checks that no timer is already running, then calls `setInterval` to update the display every 10 milliseconds. It sets `startTime = Date.now() - elapsed`, which is what allows resuming after a stop.
3. **Each tick** calculates the real time passed (`Date.now() - startTime`) instead of adding a fixed amount. This avoids drift from late ticks.
4. **Formatting** splits the milliseconds into hours, minutes, seconds, and centiseconds using `Math.floor` and the `%` operator, then adds leading zeros with `padStart`.
5. **Stop** calls `clearInterval` and resets `timerId` to `null`.
6. **Reset** stops the timer, sets `elapsed` to `0`, and updates the display.

### Time formatting example

For `3725450` milliseconds:

| Part | Calculation | Result |
|---|---|---|
| Total seconds | 3725450 ÷ 1000 | 3725 |
| Hours | 3725 ÷ 3600 | 01 |
| Minutes | (3725 % 3600) ÷ 60 | 02 |
| Seconds | 3725 % 60 | 05 |
| Centiseconds | (3725450 % 1000) ÷ 10 | 45 |

Displayed as **`01:02:05.45`**.

## What I Learned

- Using `setInterval` and `clearInterval` to run and stop repeating code
- Keeping state in variables outside functions
- Working with `Date.now()` for accurate timing
- Converting milliseconds into hours, minutes, and seconds
- Formatting numbers with `padStart`
- Selecting elements and handling click events
- Preventing bugs such as duplicate timers

## Testing Checklist

- [ ] Start makes the time run
- [ ] Clicking Start repeatedly does not change the speed
- [ ] Stop freezes the time
- [ ] Start after Stop resumes instead of restarting
- [ ] Reset works while running and while stopped
- [ ] Clicking Stop or Reset before Start causes no errors
- [ ] The time stays correct after switching to another tab and back

## Future Improvements

- [ ] Lap button with a list of recorded laps
- [ ] Single Start/Stop toggle button
- [ ] Keyboard shortcuts (Space to start or stop)
- [ ] Save laps using `localStorage`
- [ ] Countdown timer mode
- [ ] Disable buttons that do not make sense in the current state
- [ ] Dark mode toggle

## Contributing

Suggestions and improvements are welcome. Fork the repository, make your changes, and open a pull request.

## License

This project is open source and available under the [MIT License](LICENSE).

## Author

Created by **Devpreet Singh** as a beginner HTML, CSS, and JavaScript practice project.
