# Portfolio - Assignment 3

A responsive personal portfolio website built with HTML, CSS and JavaScript. This version continues Assignments 1 and 2 and adds advanced functionality: an external API, a smarter contact form, remembered visitor information, a timer and performance optimization.

## Project Description
The site introduces me (Layan Alomari, a Computer Science student at KFUPM), shows two of my projects, and has a contact form. In Assignment 3, I added a quotes section that loads data from a public API, a contact form with live checks, a visitor name that the site remembers, and a timer showing how long you have been on the page. I also optimized the images and tested the site with Lighthouse.

## Features
- **Quotes (API):** loads a random quote from the DummyJSON API, with a loading message and a friendly error message if the request fails
- **Smart contact form:** live checks for name, email and message, a character counter (up to 500), and a Send button that stays disabled until everything is valid
- **Visitor name:** the site asks for your name once, remembers it with `localStorage`, and uses it in the greeting. A "Not you?" button lets you change it
- **Time on page:** a timer in the footer shows how long you have been on the site
- **Live project search:** filter the projects as you type, with a "No projects found" message
- **Saved theme:** the dark/light mode choice is kept after a refresh
- **Time-based greeting:** "Good morning", "Good afternoon" or "Good evening"
- **Animations:** hover effects and fade-in messages
- **Responsive design:** works on laptop, tablet and phone screens

## Technologies
- HTML5
- CSS3 (Grid, Flexbox, variables, transitions, animations, media queries)
- JavaScript (no libraries or frameworks), including `fetch` with `async/await` and `localStorage`
- DummyJSON quotes API (no API key needed)

## Performance
I tested the site with Lighthouse (Mobile, on a local server) and improved it by resizing and compressing the images, adding image dimensions and adding a meta description.

| Category | Before | After |
|---|---|---|
| Performance | 99 | 100 |
| Accessibility | 100 | 100 |
| Best Practices | 100 | 100 |
| SEO | 91 | 100 |

The two project images are about 77% smaller than before. More details are in the technical documentation.

## Project Structure
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

## Setup Instructions
No installation is needed. An internet connection is needed for the quotes section.

1. Download the project: click **Code → Download ZIP** on the GitHub page and unzip it. (Or clone it with `git clone https://github.com/LayanAlomari/202351790-LayanAlomari-assignment3.git`.)
2. Open the project folder.
3. Double-click `index.html` to open it in your browser.

To test it with Lighthouse, serve the folder locally instead of opening the file directly. From the project folder, run:
```bash
python3 -m http.server 8000
```
Then open `http://localhost:8000` in Chrome.

## How to Use
- **Name:** type your name in the About section and click **Save name**. The greeting will use it, even after you refresh. Click **Not you?** to change it.
- **Projects:** type in the search box to filter the projects.
- **Quotes:** click **New Quote** to load another quote.
- **Theme:** click **Dark Mode / Light Mode** in the header. Your choice is remembered.
- **Contact:** fill in the form. The Send button turns on when every field is valid, and a confirmation message appears after you send.

## AI Usage Summary
I used Claude as my AI tool. It explained concepts (`fetch` and error handling, `localStorage`, form validation, Lighthouse) and suggested starting code for the quotes section, the form checks, the visitor name, the timer and the performance fixes, which I adapted, tested and changed to fit my project. The full details, including the usage log and declaration, are in [docs/ai-usage-report.md](docs/ai-usage-report.md).

## Documentation
- [Technical Documentation](docs/technical-documentation.md)
- [AI Usage Report](docs/ai-usage-report.md)

## Known Limitations
- The contact form has no backend, so messages are not sent.
- The quotes come from a third-party API. If it is unavailable, the site shows an error message instead.
- The theme and visitor name are saved only in the current browser, and may not be saved in private browsing mode.
- The timer starts again from 0 when the page is refreshed.