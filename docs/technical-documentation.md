# Technical Documentation

## 1. Overview
This is Assignment 4, the final version of my personal portfolio website. It is built with HTML, CSS and JavaScript only, with no frameworks. It builds on Assignments 1 to 3 and brings everything together: a responsive layout, a quote section that loads data from an external API, a contact form that really sends messages, a remembered visitor name and theme, a timer, scroll-aware navigation, and animations. The site is deployed publicly with GitHub Pages.

**Live site:** https://layanalomari.github.io/202351790-LayanAlomari-assignment4/

## 2. File Structure
```
202351790-LayanAlomari-assignment4/
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
├── presentation/
│   ├── slides.pdf
│   └── demo-video.mp4
└── .gitignore
```

| File | Purpose |
|---|---|
| `index.html` | Page structure and content |
| `css/styles.css` | Layout, colors, fonts, responsive design, dark mode and animations |
| `js/script.js` | All the behavior: greeting and visitor name, theme, search, quotes API, contact form, timer and scroll-aware navigation |
| `docs/` | Project documentation |
| `presentation/` | Slides and demo video |

## 3. Changes from Assignment 3
- The contact form now **really sends messages** through the Formspree service, with a sending state and error handling.
- Added **scroll-aware navigation**: a sticky header on larger screens, smooth scrolling and a highlighted link for the section on screen.
- Added safe helpers for `localStorage`, so the site still works if the browser blocks storage.
- Reorganized the CSS (all media queries at the end, one place for each section) and added a `prefers-reduced-motion` rule.
- [Improved fonts and spacing with a system font stack and more space between sections.]
- Centered and compacted the mobile navigation so it fits on small phones.
- **Deployed** the site with GitHub Pages.

## 4. Features

### 4.1 Greeting and visitor name (state management)
- The greeting is built by `updateGreeting()`, which uses `new Date().getHours()` to choose "Good morning", "Good afternoon" or "Good evening".
- If no name is saved, a small form asks "What should I call you?". The name is trimmed and must not be empty.
- A saved name is stored in `localStorage` under `visitorName`, and the greeting then includes it, for example "Good morning, Sara!".
- A **"Not you? Change name"** button removes the saved name and shows the form again.
- One function, `showNameState()`, decides what is visible and refreshes the greeting, so the page stays consistent.
- The name is inserted with `textContent`, so anything typed is shown as plain text.

### 4.2 Live project search
A search box above the projects filters them as the user types. The typed text is lowercased and trimmed, and each `.project-box` is shown or hidden depending on whether its text includes the search text. If nothing matches, the message "No projects found. Try a different word." is shown.

### 4.3 Quotes (external API integration)
The Quotes section loads a random quote from the public **DummyJSON** API (`https://dummyjson.com/quotes/random`), which needs no API key. The function `loadQuote()` is `async` and works in these steps:
1. Show "Loading quote..." and disable the **New Quote** button, so the user cannot send several requests at once.
2. Request the data with `fetch()`.
3. Check `response.ok`. `fetch` only fails on network errors, so an HTTP error such as 404 or 500 has to be checked manually and turned into an error.
4. Read the result with `response.json()` and show the quote and author using `textContent`.
5. If anything fails, a `catch` block shows a friendly message that says what happened and what to do next.
6. A `finally` block always re-enables the button.

A first quote loads when the page opens.

### 4.4 Contact form
The form uses `novalidate`, so the page shows its own messages instead of the browser's pop-ups.

**Rules.** Three small functions each return an error message, or an empty string when the field is valid:

| Field | Rule | Error message |
|---|---|---|
| Name | Not empty (after `trim()`) | "Please enter your name." |
| Email | Matches the pattern `name@example.com` (regular expression) | "Please enter a valid email, like name@example.com." |
| Message | At least 10 characters | "Please write a message of at least 10 characters." |

**Live behavior.**
- While typing, an error disappears as soon as its field becomes valid. When the user leaves a field, its error is shown if the field is invalid.
- A **character counter** shows `length / 500`, and the textarea has `maxlength="500"`.
- The **Send button is disabled** until all three checks pass (`Array.every()`), and a hint tells the user what to do.

**Sending the message.** On submit, `event.preventDefault()` stops the page from reloading and all fields are checked again. If they are valid:
1. The button shows "Sending..." and is disabled.
2. The form data is sent with `fetch()` (`POST`, `FormData`, `Accept: application/json`) to the **Formspree** form endpoint set in the form's `action`.
3. If the response is `ok`, a confirmation with the visitor's name is shown and the form is cleared.
4. If the request fails, a `catch` block shows "Sorry, your message could not be sent. Check your connection and try again."
5. A `finally` block puts the button back to its correct state.

**Spam protection.** The form contains a hidden field named `_gotcha`. Real visitors never see it, but bots fill it in, and Formspree ignores those messages.

### 4.5 Theme and storage
Clicking the theme button toggles the `dark-mode` class on `<body>` and saves the choice under the key `theme`. On load, the saved value is read, and if it is `"dark"` the class is added. Dark mode works by replacing the CSS color variables under `body.dark-mode`.

All storage goes through three helpers, `getStored`, `setStored` and `removeStored`, which wrap `localStorage` in `try/catch`. If the browser blocks storage, the site still works and the choice is simply not remembered.

| Key | Value | Used for |
|---|---|---|
| `theme` | `"dark"` or `"light"` | Remembering the color theme |
| `visitorName` | the visitor's name | Personalizing the greeting |

### 4.6 Time on page (timer)
The footer shows how long the visitor has been on the page. The start time is saved with `Date.now()`, and `setInterval` updates the display every second. The elapsed time is calculated from the start time, not by adding 1 each tick, so it stays correct even when the browser slows timers in a background tab. After 60 seconds, a thank-you message is shown once, using a flag variable.

### 4.7 Scroll-aware navigation (innovation)
- **Sticky header:** on screens wider than 600px, the header stays at the top while scrolling (`position: sticky`). On phones the header stacks and is tall, so it scrolls normally.
- **Smooth scrolling:** `html { scroll-behavior: smooth; }`. `scroll-margin-top` on sections keeps a heading from hiding under the sticky header.
- **Active link:** an `IntersectionObserver` watches each section. A section counts as "on screen" when it crosses the middle of the window (`rootMargin: "-45% 0px -50% 0px"`), and its nav link gets the `active` class using `classList.toggle`. This avoids running code on every scroll event.
- Smooth scrolling and animations are switched off for users whose system asks for reduced motion (`prefers-reduced-motion`).

### 4.8 Animations and transitions
- **Hover effects:** project boxes lift up with a shadow, and nav links and buttons change smoothly (CSS `transition`). A disabled button does not react to hovering.
- **Fade-in:** project boxes, error messages, the success message and the "No projects found" message use a `fade-in` animation (0.4 seconds). Error paragraphs use `:empty { display: none; }`, so they stay hidden until text is added.

## 5. Design and Responsive Layout
- **Colors:** defined once as CSS variables in `:root`, and replaced in dark mode.
- **Layout:** Flexbox for the header, the footer and the form; CSS Grid for the projects (two columns, one column at 600px and below).
- **Breakpoints:** tablet (768px) and mobile (600px). On phones, the navigation is centered and its links are smaller so that all four fit on one row at 375px, and the footer content is centered.
- [**Fonts and spacing:** a system font stack (`system-ui, "Segoe UI", Roboto, ...`) is used, so no font files need to be downloaded, and sections have generous padding.]
- All media queries are at the end of the stylesheet, so they correctly override the base rules.

## 6. Performance
### Testing method
I tested the site with Lighthouse in Chrome DevTools (Navigation mode, Mobile), first on a local server and then on the live GitHub Pages site.The final tests were run in an Incognito window so browser extensions did not affect the results. Lighthouse scores are estimates and may vary a little between runs.

### Results

| Category | Start of Assignment 3 | End of Assignment 3 (local) | Final (live site) |
|---|---|---|---|
| Performance | 99 | 100 | 98 |
| Accessibility | 100 | 100 | 100 |
| Best Practices | 100 | 100 | 100 |
| SEO | 91 | 100 | 100 |

### What was done
- **Compressed and resized the project screenshots** (1562x808 pixels displayed at 680x352) to 800 pixels wide JPEG files. `daleel-kfupm` went from 237.7 KiB to about 25 KiB and `flying-stars` from 147.0 KiB to about 64 KiB, about 77% smaller.
- **Added `width` and `height` to the images** so the page does not shift while they load, and used `loading="lazy"`.
- **Added a meta description**, which fixed the only failed SEO check.
- **Removed unused files and code**, and kept macOS `.DS_Store` files out of the repository with `.gitignore`.
- **Grouped repeated code:** the form checks are written once and reused, and shared CSS rules are combined.
- **No libraries, frameworks or web fonts**, so there are no extra downloads.
- The script is loaded at the end of `<body>`, and the quote request does not block the first display of the page.

### Suggestions I decided not to apply
- **Minify JavaScript (about 3 KiB saving):** I kept `script.js` readable, because the saving is small and minified code is hard to read.
- **Unused JavaScript reported by Lighthouse:** it came from a browser extension, not my code.
- **Efficient cache lifetimes (87 KiB):** GitHub Pages controls how long files are cached, so this cannot be changed in the project.
- **Render-blocking requests:** the stylesheet must load before the page is shown, so that the page is not displayed unstyled.

## 7. Deployment
The site is deployed with **GitHub Pages**:
1. The code is merged into the `main` branch.
2. In the repository's **Settings → Pages**, the source is set to **Deploy from a branch**, using `main` and the root folder.
3. GitHub builds and publishes the site, usually within a minute or two. Any later merge into `main` updates it the same way.

All file paths are relative (`css/styles.css`, `assets/images/...`), so the site works under the repository's address. The Quotes section needs an internet connection.

## 8. Testing and Compatibility

| Area | What I tested |
|---|---|
| Quotes | Loading on open and with the button; the error message by setting the browser to Offline in DevTools |
| Contact form | Empty fields, a bad email, a short message, the 500-character limit, Send staying disabled until valid, a real message reaching my inbox, and the error message when offline |
| Visitor name | Empty name, saving a name, refreshing, and "Not you?" |
| Timer | Counting up, and the thank-you message after one minute |
| Search, theme, animations | Matching and non-matching searches, saving the theme, hover effects and fade-ins |
| Navigation | Highlighting while scrolling, smooth scrolling from the links, and the header at different widths |

**Browsers and devices**

| Environment | Result |
|---|---|
| Chrome (laptop) | Works |
| Safari (laptop) | Works |
| Real phone ([iPhone / Android]) | Works |
| DevTools at 320, 375, 440, 768 and 1280 px | Works |

I also checked the dark theme and the browser Console for errors.

## 9. Error Handling Summary

| Situation | What the user sees |
|---|---|
| The quotes API fails or the user is offline | A friendly message that explains the problem and says to click New Quote to try again |
| The contact form cannot send | "Sorry, your message could not be sent. Check your connection and try again." The button comes back so they can retry |
| Invalid form input | A specific message next to the field, and Send stays disabled |
| No search results | "No projects found. Try a different word." |
| Empty visitor name | "Please type a name first." |
| Browser storage is blocked | The site works normally, and the theme and name are simply not remembered |

## 10. Known Limitations and Future Work

### Limitations
- Contact messages are sent through **Formspree**, a third-party service. The visitor's name, email and message pass through it, and the free plan has a monthly limit on messages. If the service is unavailable, the user sees the error message.
- The quotes come from a third-party API. If it is down or changes, the site shows an error message instead of a quote.
- The theme and visitor name are saved only in the current browser, and are not shared between devices.
- The timer starts again from 0 when the page is refreshed.
- On phones the header scrolls with the page, so that it does not cover too much of the small screen.
- The email check is a basic pattern and does not prove the address exists.
- The project search only checks the title and description text.

### Planned for future work
- Add more projects, each with technology tags and links.
- A larger introduction (hero) section.
- A language switch (English and Arabic).
- A custom domain name.
- A full accessibility review.

## 11. User Guide
- **Greeting:** type your name in the About section and click **Save name**. The greeting uses it, even after you refresh. Click **Not you?** to change it.
- **Projects:** type in the search box to filter the projects.
- **Quotes:** click **New Quote** for another quote.
- **Contact:** fill in the form. The Send button turns on when every field is valid. A confirmation appears when the message has been sent.
- **Theme:** click **Dark Mode / Light Mode** in the header.
- **Navigation:** use the links in the header. On a laptop, the header stays at the top, and the link of the section you are viewing is highlighted.