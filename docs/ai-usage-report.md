## AI Usage Report - Assignment 4

## 1. Tools Used & Use Cases

### Claude
I used Claude as my only AI tool for this assignment, as a tutor and code helper. I used it to:
- Understand the assignment, compare ideas for the innovation requirement by difficulty, and plan the work in phases
- Set up the new repository: copying my Assignment 3 files, the `.gitignore` entries and a working branch
- Get starting code and explanations for the new features:
  - a contact form that really sends messages, using the Formspree service with `fetch`, a sending state, an error message and a hidden spam-trap field
  - scroll-aware navigation (a sticky header, smooth scrolling and a highlighted link for the section on screen)
  - safe helpers around `localStorage`, so the site still works when the browser blocks storage
- Reorganize my CSS into a cleaner order with all media queries at the end, and review my full JavaScript file
- Suggest fonts and spacing improvements and fix problems with the mobile header at small screen widths
- Understand deployment with GitHub Pages and how to read Lighthouse results for the live site
- Write a first draft of the technical documentation and of this report's structure
- Help with Git: commit messages that credit AI, merging a branch into `main` with a pull request, and deciding when to merge
- Suggest an outline for my presentation: the number of slides, what to put on each slide, the timing for the 5-7 minute limit, and tips for the visuals and the recording

I did not use any other AI tool.

## 2. Benefits & Challenges

### Benefits
- I could ask follow-up questions and get explanations at my level, for example why a disabled button still reacted to hovering and what `IntersectionObserver` does.
- Claude compared several innovation ideas by how easy they were, which helped me choose two features that I could finish and that added real value.
- It spotted problems in my code that I had not noticed, such as a CSS ordering bug and the risk that blocked storage would stop my whole script.
- It helped me read the Lighthouse report and understand which suggestions mattered and which I could ignore.
- Having the work split into phases helped me stay organized.

### Challenges
- **Searching for a service.** When I looked for Formspree, search results showed ads for unrelated companies, and I once ended up on a different form service (Cognito Forms) with a sign-up survey. Claude helped me recognize that it was the wrong site, and I typed the real address myself.
- **Layouts that worked on one phone size but not another.** The navigation looked right at iPhone 16 width but wrapped badly at iPhone SE width. I found this by testing different device sizes, and then fixed it with Claude's suggestion.
- **Suggestions I did not want.** Claude offered a sticky compact header for phones and extra design polish. I decided to keep the header scrolling on phones and to skip the extra design work so I could finish the documentation and presentation.
- **Code could not be tested by the AI.** Claude could not run my code in a browser, so I had to test every feature myself, including sending a real message and checking the error handling by going offline.

## 3. Learning Outcomes
- **JavaScript:** how to send form data with `fetch` using `POST` and `FormData`, how to handle success and failure with `try/catch/finally`, how `IntersectionObserver` works, and how to protect code that depends on `localStorage`.
- **CSS:** how `position: sticky` and `scroll-margin-top` work together, why the order of rules matters (the cascade), why media queries belong at the end, and how to make a layout work on small screens.
- **Services and privacy:** how a third-party form service works, what data it receives, and why that should be documented.
- **Deployment:** how GitHub Pages publishes the `main` branch, and why a change is only visible on the live site after it is merged.
- **Performance:** how Lighthouse results differ between a local server and a live site, and which suggestions I cannot control.
- **Workflow:** testing on different devices, committing in small steps with the AI credit, and keeping notes as I work so the usage log is accurate.

## 4. Responsible Use & Modifications
I did not copy the AI output without checking it. I reviewed each suggestion, made my own decisions and tested the results:

- I chose which innovation features to build, based on the options and difficulty levels Claude gave me.
- I created the Formspree account, entered my own form address and tested it by sending a real message to my inbox, and I tested the error message by going offline.
- I decided to keep the header scrolling on phones, and to skip extra design polish.
- I found the navigation problem on small phones by testing different device widths, and I applied and checked the fix.
- I checked the new JavaScript file and CSS file in the browser after replacing them.
- I deployed the site myself and ran Lighthouse on the live link, and I recorded the scores for the documentation.
- I asked questions about things I did not understand, such as what the Formspree and Cognito pages were, and whether a change had to be merged before it appeared on the live site.
- I credited AI help in my commit messages with an `Assisted-by` line, and I will list all of it in the usage log.
- I used Claude's slide outline as a starting point, and changed it to fit my own project.

I understand the code in my project and can explain how each part works.

## Usage Log

| ID | Tool (model) | Date | Purpose | Files affected | What I changed and how I verified it |
|---|---|---|---|---|---|
| C01 | Claude (Sonnet 5.5) | 2026-11-27 | My conversation for this assignment: planning, Git help, explanations, debugging, deployment and Lighthouse help, and documentation | all files | Full conversation is in `conversations/` in the evidence ZIP |
| A01 | Claude (Sonnet 5.5) | 2026-11-27 | Contact form that sends messages through Formspree: the `fetch` request, the sending state, the error message and the hidden spam-trap field | `index.html`, `js/script.js`, `css/styles.css` | I created the Formspree account and entered my own form address. I tested a real message that reached my inbox, the validation, and the error message by setting the browser to Offline. Evidence: `artifacts/index.html`, `artifacts/script.js`, `artifacts/styles.css` |
| A02 | Claude (Sonnet 5.5) | 2026-11-27 | Scroll-aware navigation: sticky header, smooth scrolling and a highlighted link for the section on screen | `css/styles.css`, `js/script.js` | I tested scrolling, clicking each link, dark mode and different widths. Evidence: `artifacts/styles.css`, `artifacts/script.js` |
| A03 | Claude (Sonnet 5.5) | 2026-11-27 | Reorganized CSS file, with all media queries at the end and a fix for a disabled button reacting to hovering | `css/styles.css` | I replaced my file with the new one and compared the page before and after in light and dark mode and at phone width. Evidence: `artifacts/styles.css` |
| A04 | Claude (Sonnet 5.5) | 2026-11-27 | Font and spacing suggestions (system font stack, section padding) | `css/styles.css` | Applied them and checked each section. Evidence: `artifacts/styles.css` |
| A05 | Claude (Sonnet 5.5) | 2026-11-27 | Review of my JavaScript file, safe `localStorage` helpers, and a regrouped version of the script | `js/script.js` | I replaced my script with the new version and tested the name, the theme, the quote, the form and the navigation, and checked the Console for errors. Evidence: `artifacts/script.js` |
| A06 | Claude (Sonnet 5.5) | 2026-11-27 | Fix for the mobile navigation wrapping at small phone widths | `css/styles.css` | I found the problem by testing iPhone SE width, applied the fix and checked 375, 440 and narrower widths. I decided to keep the header scrolling on phones instead of making it sticky. Evidence: `artifacts/styles.css` |
| A07 | Claude (Sonnet 5.5) | 2026-11-27 | Guidance for deploying with GitHub Pages and for reading the Lighthouse results of the live site | none (settings on GitHub) | I did the deployment myself, tested the live link, ran Lighthouse on it and recorded the scores. Evidence: the conversation |
| A08 | Claude (Sonnet 5.5) | 2026-11-27 | First draft of the technical documentation, and notes about the live Lighthouse results | `docs/technical-documentation.md` | I checked each statement against my code and filled in my own test results. Evidence: `artifacts/technical-documentation.md` |
| A09 | Claude (Sonnet 5.5) | 2026-11-27 | First draft of the README | `README.md` | I checked the links and the scores. Evidence: `artifacts/README.md` |
| A10 | Claude (Sonnet 5.5) | 2026-11-27 | First draft of the first four sections of this report | `docs/ai-usage-report.md` | I checked each statement against my code. Evidence: `artifacts/ai-usage-report.md` |
| A11 | Claude (Sonnet 5.5) | 2026-11-27 | Outline for the presentation slides (number of slides, content of each, timing, visual and recording tips) | `presentation/slides.pdf` | I wrote the slide text in my own words, chose the screenshots and the demo order. I rehearsed with a timer to stay within 5-7 minutes. Evidence: the conversation |

## Declaration

I declare that this report and the attached evidence document all of my AI use in this assignment, with complete and unedited conversations, and that I understand and can explain all the code I submitted. I understand that undeclared AI use or a false declaration will be treated as plagiarism according to KFUPM regulations.

Name: Layan Alomari
ID: 202351790
Date: 2026-11-27