# Personal Web Application - Assignment 4

My personal portfolio website, built with HTML, CSS and JavaScript only. This is the final version, bringing together everything from Assignments 1 to 3 in a deployed, responsive and polished web application.

**Live site:** https://layanalomari.github.io/202351790-LayanAlomari-assignment4/

## Project Description
The site introduces me (Layan Alomari, a Computer Science student at KFUPM), shows two of my projects, and lets visitors read a quote and send me a message. It has a responsive layout for laptops, tablets and phones, a dark and light theme, and a set of interactive features. It is deployed publicly with GitHub Pages.

## Features
- **Contact form that really sends:** live checks for the name, email and message, a character counter, and a Send button that stays disabled until everything is valid. Messages are sent to my inbox through the Formspree service, with a "Sending..." state and a friendly error message if something fails
- **Scroll-aware navigation:** a sticky header on larger screens, smooth scrolling, and the link of the section you are viewing is highlighted
- **Quotes (external API):** loads a random quote from the DummyJSON API, with a loading message and an error message
- **Remembered visitor name and theme:** the site asks for your name once and uses it in the greeting, and it remembers your dark or light theme. Both are saved in the browser, and the site still works if the browser blocks storage
- **Live project search:** filters the projects as you type, with a "No projects found" message
- **Timer:** shows how long you have been on the page
- **Animations:** hover effects and fade-in messages
- **Responsive design:** works on laptop, tablet and phone screens, and respects the "reduced motion" setting

## Technologies
- HTML5
- CSS3 (Grid, Flexbox, variables, transitions, animations, media queries)
- JavaScript (no libraries or frameworks), including `fetch` with `async/await`, `localStorage` and `IntersectionObserver`
- DummyJSON quotes API (no key needed) and the Formspree form service
- GitHub Pages for deployment

## Performance
Lighthouse results for the live site (Mobile):

| Performance | Accessibility | Best Practices | SEO |
|---|---|---|---|
| 98 | 100 | 100 | 100 |

The project images were resized and compressed (about 77% smaller), and the page uses no frameworks or web fonts. More details are in the technical documentation.

## Project Structure
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

## Setup Instructions
No installation is needed, and you can also just open the live site. An internet connection is needed for the quotes and the contact form.

1. Download the project: click **Code → Download ZIP** on the GitHub page and unzip it. (Or clone it with `git clone https://github.com/LayanAlomari/202351790-LayanAlomari-assignment4.git`.)
2. Open the project folder.
3. Double-click `index.html` to open it in your browser.

To run it on a local server (for example to test with Lighthouse), run this in the project folder and open `http://localhost:8000`:
```bash
python3 -m http.server 8000
```

Note: the contact form sends real messages to my inbox, even when the site is run locally.

## How to Use
- **Navigation:** use the links in the header. The link of the section you are viewing is highlighted.
- **Name:** type your name in the About section and click **Save name**. The greeting will use it, even after you refresh. Click **Not you?** to change it.
- **Projects:** type in the search box to filter the projects.
- **Quotes:** click **New Quote** for another quote.
- **Theme:** click **Dark Mode / Light Mode** in the header. Your choice is remembered.
- **Contact:** fill in the form. The Send button turns on when every field is valid, and a confirmation appears when the message has been sent.

## AI Usage Summary
I used Claude as my only AI tool. It explained concepts (sending form data with `fetch`, `IntersectionObserver`, CSS ordering, deployment, Lighthouse) and suggested starting code for the contact form, the scroll-aware navigation, the safe storage helpers and the reorganized CSS, which I adapted, tested and changed to fit my project. Claude also suggested the structure of my presentation slides (the number of slides, the content of each one and the timing).The full details, including the usage log and declaration, are in [docs/ai-usage-report.md](docs/ai-usage-report.md).

## Documentation and Presentation
- [Technical Documentation](docs/technical-documentation.md)
- [AI Usage Report](docs/ai-usage-report.md)
- [Presentation slides](presentation/slides.pdf)
- [Demo video](presentation/demo-video.mp4)

## Known Limitations
- Contact messages go through the Formspree service, which has a monthly limit on the free plan. If it is unavailable, the site shows an error message.
- The quotes come from a third-party API. If it is unavailable, the site shows an error message instead.
- The theme and visitor name are saved only in the current browser.
- The timer starts again from 0 when the page is refreshed.
- On phones the header scrolls with the page.