# AI Usage Report - Assignment 3

## 1. Tools Used & Use Cases

### Claude
I used Claude as my only AI tool for this assignment, as a tutor and code helper. I used it to:
- Break the assignment into phases and compare API options for my portfolio
- Set up the repository work: the `.gitignore` template choice, copying my Assignment 2 files, and creating a working branch
- Get starting code for the new features:
  - a Quotes section that loads data from an external API, with a loading message and an error message
  - a contact form with live checks, a character counter and a Send button that stays disabled until the form is valid
  - remembering the visitor's name with `localStorage`
  - a timer showing how long the visitor has been on the page
  - the footer layout, with the copyright on the left and the timer on the right
- Understand how the code works: `fetch` with `async/await`, `try/catch/finally`, `response.ok`, array methods like `every()` and `forEach()`, `localStorage`, `setInterval` and `Date.now()`
- Format my code with correct indentation in VS Code
- Debug problems, such as a duplicate-variable error in my JavaScript and the Lighthouse "can only audit HTTP or HTTPS pages" error
- Improve performance: run Lighthouse, read its report, resize and compress my images, add image dimensions and add a meta description
- Check whether `.DS_Store` files were committed to my repository
- Write first drafts of the technical documentation and the README, and the structure of this report

I did not use any other AI tool for this assignment. **[check: add any other tool you used]**

## 2. Benefits & Challenges

### Benefits
- I could ask follow-up questions, such as why the old form code had to be removed and what `.DS_Store` is, and get explanations at my level.
- Claude compared several API options and tested a few quote APIs before I chose one, which saved me from picking one that did not work in a browser.
- It helped me read the Lighthouse report and understand which suggestions mattered. Resizing the images made my two screenshots about 77% smaller.
- It showed me a step-by-step way to write logic (for example, the form checks as small functions that are reused).
- Splitting the work into phases helped me stay organized.

### Challenges
- **My ideas did not always match the suggestions.** Claude suggested a saved-quotes feature with filtering and sorting, but I did not like it because it did not fit a portfolio. I asked for other options and chose a different set of features. **[check: say whether you added the saved-quotes code or not]**
- **Generated code needed careful pasting.** I added the new contact form code without removing the old version, and the file had duplicate variable declarations, which caused an error in the editor and would have stopped the whole script. I had to find both versions and delete the old one.
- **Some instructions were incomplete.** The first Lighthouse steps did not mention that the page has to be served over HTTP, so Lighthouse showed an error when I opened the file directly. I needed to run a local server.
- **Not every suggestion was worth applying.** Lighthouse suggested minifying my JavaScript, which would save very little and make my code hard to read, so I decided not to do it. Another suggestion came from a browser extension, not from my code.
- **I had to test everything myself.** The code worked in the examples, but I tested each feature and checked the browser Console to be sure it worked in my project.

## 3. Learning Outcomes
- **APIs:** how to request data with `fetch`, why `response.ok` must be checked separately, and how to show loading and friendly error messages.
- **JavaScript:** how `try/catch/finally` works, how to use arrays of objects with `forEach` and `every`, how to use `Date.now()` and `setInterval` for a timer, and why computing time from a start time is more reliable than adding one each second.
- **State:** how to store and read data with `localStorage`, and how one function can keep the page consistent with the saved state.
- **Forms:** how to validate in steps (live, when leaving a field, and again on submit) and how to write each rule once.
- **Performance:** how to use Lighthouse, why large images slow a page, how resizing, compression and image dimensions help, and why some suggestions can be skipped.
- **Git:** the difference between a file being ignored and a file being tracked, and how to stop tracking a file.
- **Workflow:** keeping a record of each AI use while I work, so that I can document it honestly.

## 4. Responsible Use & Modifications
I did not copy the AI output without checking it. I reviewed each suggestion, made my own decisions and tested the results:

- I rejected the saved-quotes idea and chose the contact form checks, the timer and the visitor name instead.
- I asked for a different footer layout because I did not like the first one, and applied the new CSS.
- I fixed the duplicate-variable error myself by finding and removing the old form code.
- I decided not to apply the JavaScript minification suggestion, and I wrote down why in the technical documentation.
- I resized and compressed my own screenshots, checked the new file sizes and updated the image tags with the real width and height values.
- I ran Lighthouse before and after my changes and recorded the scores.
- I tested each feature: loading quotes and the error message with the browser set to offline, the form rules and the character counter, saving and clearing the visitor name, the timer, and the layout at different screen sizes.
- I asked questions about parts I did not understand, such as why the old code had to be removed and how to check `.DS_Store`.
- I credited AI help in my commit messages with an `Assisted-by` line, and listed it in the usage log below.

I understand the code in my project and can explain how each part works.

## Usage Log

| ID | Tool (model) | Date | Purpose | Files affected | What I changed and how I verified it |
|---|---|---|---|---|---|
| C01 | Claude (Sonnet 5.5) | 2026-11-21 | My conversation for this assignment: planning, API options, Git help, explanations, debugging, Lighthouse help and documentation | all files | Full conversation is in `conversations/` in the evidence ZIP |
| A01 | Claude (Sonnet 5.5) | 2026-11-21 | Quotes section that fetches a random quote from the DummyJSON API, with a loading message and an error message | `index.html`, `js/script.js`, `css/styles.css` | Tested that quotes load and the button gives new ones; tested the error message by setting the browser to Offline in DevTools. Evidence: `artifacts/index.html`, `artifacts/script.js`, `artifacts/styles.css` |
| A02 | Claude (Sonnet 5.5) | 2026-11-21 | Saved-quotes feature with search and sort (generated but not used) | none in the final project | I did not like the idea because it did not fit a portfolio, so I asked for other options and did not add it. Evidence: `artifacts/script.js`, `artifacts/styles.css`, `artifacts/index.html` |
| A03 | Claude (Sonnet 5.5) | 2026-11-21 | Contact form live checks, character counter and Send button that stays disabled until valid | `index.html`, `js/script.js`, `css/styles.css` | I first added the new code without removing the old form code, which caused a duplicate-variable error, so I found both versions and deleted the old one. Tested empty fields, a bad email, a short message, the 500-character limit and a valid submit. Evidence: `artifacts/index.html`, `artifacts/script.js`, `artifacts/styles.css` |
| A04 | Claude (Sonnet 5.5) | 2026-11-21 | Time-on-page timer | `index.html`, `js/script.js` | Watched it count and shortened the 60-second limit temporarily to check the thank-you message. Evidence: `artifacts/index.html`, `artifacts/script.js` |
| A05 | Claude (Sonnet 5.5) | 2026-11-21 | Visitor name remembered with `localStorage`, and the greeting using it | `index.html`, `js/script.js`, `css/styles.css` | Tested saving a name, an empty name, refreshing, and the "Not you?" button. Evidence: `artifacts/index.html`, `artifacts/script.js`, `artifacts/styles.css` |
| A06 | Claude (Sonnet 5.5) | 2026-11-21 | Footer layout with the copyright on the left and the timer on the right | `css/styles.css` | I asked for this layout because I did not like the first version, then checked it at desktop and phone width. Evidence: `artifacts/styles.css` |
| A07 | Claude (Sonnet 5.5) | 2026-11-21 | Performance fixes: resizing and compressing images, image width and height, meta description, `.DS_Store` check | `assets/images/`, `index.html` | I ran Lighthouse before and after (Performance 99 to 100, SEO 91 to 100), resized the images with the `sips` command, checked the new file sizes and used the real dimensions. I skipped the JavaScript minify suggestion. Evidence: `artifacts/index.html` and the conversation |
| A08 | Claude (Sonnet 5.5) | 2026-11-21 | First draft of the technical documentation | `docs/technical-documentation.md` | I checked each statement against my code. Evidence: `artifacts/technical-documentation.md` |
| A09 | Claude (Sonnet 5.5) | 2026-11-21 | First draft of the README | `README.md` | I checked each statement against my code. Evidence: `artifacts/README.md` |
| A10 | Claude (Sonnet 5.5) | 2026-11-21 | First draft of the first four sections of this report | `docs/ai-usage-report.md` | I checked each statement against my code. Evidence: `artifacts/ai-usage-report.md` |

## Declaration

I declare that this report and the attached evidence document all of my AI use in this assignment, with complete and unedited conversations, and that I understand and can explain all the code I submitted. I understand that undeclared AI use or a false declaration will be treated as plagiarism according to KFUPM regulations.

Name: Layan Alomari
ID: 202351790
Date: 2026-11-21