# Technical Documentation

## 1. Overview
This is Assignment 3 of my portfolio. It builds on the Assignment 2 site (HTML, CSS, JavaScript, no frameworks or backend) and adds advanced functionality: a quote section that loads data from an external API, a contact form with live checks and a character counter, a visitor name that is remembered, and a timer showing how long the visitor has been on the page. I also optimized the site's performance and measured it with Lighthouse.

## 2. File Structure
```
202351790-LayanAlomari-assignment3/
├── README.md
├── index.html
├── css/
│   └── styles.css
├── js/
│   └── script.js
├── assets/
│   └── images/
│       ├── flying-stars.jpg
│       └── daleel-kfupm.jpg
├── docs/
│   ├── ai-usage-report.md
│   └── technical-documentation.md
└── .gitignore
```

| File | Purpose |
|---|---|
| `index.html` | Page structure and content |
| `css/styles.css` | Layout, colors, responsive design, dark mode and animations |
| `js/script.js` | Greeting, theme toggle, project search, quotes API, form checks, visitor name and timer |
| `docs/` | Project documentation |

## 3. Changes from Assignment 2
- Added a **Quotes** section that fetches a random quote from an external API, with loading and error messages.
- Rebuilt the contact form checks: live validation, a character counter and a Send button that stays disabled until the form is valid.
- Added a **visitor name** that is saved in `localStorage` and used in the greeting.
- Added a **timer** in the footer showing the time on the page.
- Moved the footer to a two-sided layout (copyright on the left, timer on the right).
- Optimized the images, added a meta description and removed unused files (see section 6).

## 4. Features

### 4.1 Live project search
A search box above the projects filters them as the user types.

- A listener on the `input` event runs on every keystroke.
- The typed text is lowercased and trimmed, so the search ignores capital letters.
- For each `.project-box`, the script checks whether the box's text (title and description) contains the search text, using `includes()`.
- Matching boxes are shown and the others are hidden with the `hidden` property.
- A counter tracks how many projects match. If it is 0, the message "No projects found. Try a different word." is shown (empty state).

### 4.2 Quotes (external API integration)
The Quotes section loads a random quote from the public **DummyJSON** API (`https://dummyjson.com/quotes/random`), which needs no API key. It returns an object with a `quote` and an `author`.

The function `loadQuote()` is `async` and works in these steps:
1. Show "Loading quote..." and disable the **New Quote** button so the user cannot send several requests at once.
2. Request the data with `fetch()`.
3. Check `response.ok`. `fetch` only fails on network errors, so an HTTP error such as 404 or 500 has to be checked manually and turned into an error.
4. Read the result with `response.json()` and show the quote and author using `textContent`.
5. If anything fails, a `catch` block shows a friendly message: "Sorry, we could not load a quote. Check your internet connection and click New Quote to try again." This tells the user what happened and what to do next.
6. A `finally` block always re-enables the button, whether the request worked or not.

A first quote loads when the page opens, and the button loads a new one.

### 4.3 Contact form (complex logic and live validation)
The form uses `novalidate`, so the page shows its own messages instead of the browser's pop-ups. The logic has several steps:

**Rules.** Three small functions each return an error message, or an empty string when the field is valid:

| Field | Rule | Error message |
|---|---|---|
| Name | Not empty (after `trim()`) | "Please enter your name." |
| Email | Matches the pattern `name@example.com` (regular expression) | "Please enter a valid email, like name@example.com." |
| Message | At least 10 characters | "Please write a message of at least 10 characters." |

**Live behavior.**
- While typing, an error disappears as soon as its field becomes valid.
- When the user leaves a field, its error is shown if the field is invalid.
- A **character counter** under the message shows `length / 500`, and the textarea has `maxlength="500"`.
- The **Send button is disabled** until all three checks pass, and a hint ("Fill in every field correctly to enable the Send button.") tells the user what to do. The hint is hidden once the form is valid. The button is enabled with `Array.every()`.

**On submit.** `event.preventDefault()` stops the page from reloading, and all fields are checked again as a safety step. If everything is valid, a confirmation message with the visitor's name is shown ("Thanks, NAME! Your message was submitted."), the form is cleared and the button is disabled again. The name is inserted with `textContent` so it is treated as plain text.

The same check functions are used for the live checks and for the submit, so the rules are written only once.

### 4.4 State management
The site remembers information between visits with `localStorage`:

| Key | Value | Used for |
|---|---|---|
| `theme` | `"dark"` or `"light"` | Remembering the color theme |
| `visitorName` | the visitor's name | Personalizing the greeting |

**Theme.** Clicking the theme button toggles the `dark-mode` class on `<body>` and saves the choice. On load, the saved value is read, and if it is `"dark"` the class is added and the button text becomes "Light Mode". Dark mode works by replacing the CSS color variables under `body.dark-mode`.

**Visitor name.**
- If no name is saved, a small form asks "What should I call you?". The name is trimmed and must not be empty, otherwise a message is shown.
- Saving stores the name in `localStorage`, hides the form and shows a **"Not you? Change name"** button.
- The greeting is built by `updateGreeting()`, which picks "Good morning", "Good afternoon" or "Good evening" from `new Date().getHours()` and adds the name when one is saved, for example "Good morning, Sara!".
- "Not you?" removes the saved name with `removeItem` and shows the form again.
- One function, `showNameState()`, decides what is visible and refreshes the greeting, so the page stays consistent.

### 4.5 Time on page (timer)
The footer shows how long the visitor has been on the page, for example "Time on this page: 1:05".

- The start time is saved with `Date.now()` when the page loads.
- `setInterval` runs an update function every second.
- Each update calculates the elapsed seconds from the start time (not by adding 1 each tick), so the value stays correct even when the browser slows timers in a background tab.
- Minutes and seconds are calculated, and `padStart` adds a leading zero to the seconds.
- After 60 seconds, a message is shown once ("Thanks for staying a while! Feel free to send me a message."). A flag variable prevents it from repeating.

### 4.6 Animations and transitions
- **Hover effects:** project boxes lift up with a shadow, and nav links and buttons change smoothly (CSS `transition`).
- **Fade-in:** project boxes, error messages, the success message and the "No projects found" message use a `fade-in` animation (`@keyframes`, 0.4 seconds). Error paragraphs use `:empty { display: none; }`, so they stay hidden until text is added and the animation plays when they appear.

## 5. Responsive Design
Flexbox is used for the header, the footer and the form, and CSS Grid for the projects (two columns, one column at 600px and below). Media queries adapt the layout for tablet (768px) and mobile (600px). On small screens, the footer content is centered instead of split left and right. The Quotes section, the visitor name box and the form messages use the same layout rules.

## 6. Performance
### Testing method
I tested the site with Lighthouse in Chrome DevTools (Navigation mode, Mobile) while serving the project locally at `http://localhost:8000`. [I ran the final test in an Incognito window so browser extensions did not affect the results.] Lighthouse scores are estimates and may vary a little between runs.

### Results

| Category | Before | After |
|---|---|---|
| Performance | 99 | 100 |
| Accessibility | 100 | 100 |
| Best Practices | 100 | 100 |
| SEO | 91 | 100 |

### Changes made
- **Compressed and resized the project screenshots.** Lighthouse reported that the images were much larger than the size they are displayed at (for example 1562x808 pixels shown at 680x352). I resized both to 800 pixels wide and saved them as JPEG files. `daleel-kfupm` went from 237.7 KiB to about 25 KiB, and `flying-stars` from 147.0 KiB to about 64 KiB, so the two images together are about 77% smaller.
- **Added `width` and `height` to the images** so the browser reserves their space and the page does not shift while they load. The CSS (`width: 100%; height: auto`) keeps them responsive. The images also use `loading="lazy"`.
- **Added a meta description**, which fixed the only failed SEO check.
- **Removed unused files**, including the old PNG images, and kept macOS `.DS_Store` files out of the repository with `.gitignore`.
- **Grouped repeated code.** The contact form uses one set of check functions for both the live checks and the submit check, and the same listeners are attached to all fields with a loop.

### Suggestions I decided not to apply
- **Minify JavaScript (about 3 KiB saving).** I kept `script.js` readable, since the saving is small and minified code is hard to read and maintain.
- **Reduce unused JavaScript (39 KiB).** This came from a browser extension, not from my code, and it disappeared when testing without extensions.
- **Back/forward cache warning.** This is a diagnostic that does not affect the score. [Add what you found if you checked the reasons.]

### Other performance choices
- The script is loaded at the end of `<body>`, so it does not block the page from showing.
- The quote request does not block the first display of the page, and a loading message shows while it runs.
- The site uses no external libraries or frameworks.

## 7. Testing
- **Quotes:** loaded a quote on page open and with the button. Tested the error handling by setting the browser to Offline in DevTools, which showed the friendly message, and checked that the button worked again after going back online.
- **Contact form:** left fields empty and clicked away, entered an invalid email, typed a short message, checked the counter up to 500, checked that Send stays disabled until everything is valid, and submitted valid data to see the confirmation.
- **Visitor name:** tried saving an empty name, saved a name and refreshed to check that it was remembered, and used "Not you?" to remove it.
- **Timer:** watched it count up, and temporarily shortened the 60-second limit to check the thank-you message.
- **Search, theme and animations:** searched for matching and non-matching words, switched the theme and refreshed, and checked hover effects and fade-ins.
- Checked dark mode and the layout at laptop, tablet and phone sizes in Chrome DevTools.
- Checked the browser Console for errors.

## 8. Known Limitations
- The contact form has no backend, so messages are not actually sent or stored.
- The quotes come from a third-party API. If it is down or changes, the site shows the error message instead of a quote.
- The quotes are random and have no categories.
- The email check is a basic pattern and does not prove the address exists.
- The theme and visitor name are saved only in the current browser. They are not shared between devices, and they may not be saved in private browsing mode.
- The timer starts again from 0 when the page is refreshed.
- Lighthouse was run on a local server, so real-world loading times on the internet may be different.