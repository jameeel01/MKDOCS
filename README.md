# Firebase User Documentation for COMP 1800

A comprehensive how-to guide for setting up Google Firebase in a COMP 1800 web project, written for first-term BCIT CST students.

**Live Site:** [https://jameeel01.github.io/MKDOCS](https://jameeel01.github.io/MKDOCS)

---

## About This Project

This repository contains a user documentation guide that walks new CST students through the full Firebase setup process for their COMP 1800 team project. The guide covers four core tasks:

1. **Setting Up Firebase** — Creating a Firebase project, registering a web app, installing the Firebase SDK via npm, and connecting it to a Vite-based project.
2. **Setting Up Cloud Firestore** — Creating a Firestore database, understanding collections and documents, and performing read/write operations using the v9 modular SDK.
3. **Setting Up Firebase Authentication** — Enabling Email/Password sign-in, building login and sign-up functionality, and protecting pages with authentication guards.
4. **Deploying to Firebase Hosting** — Installing the Firebase CLI, building with Vite, and deploying to a live `.web.app` URL.

The guide also includes a glossary of key terms, a troubleshooting section with 12 common issues and solutions, and this README documenting our process.

---

## Intended Audience

First-term BCIT CST students entering the program in September 2026 who are building a web application with HTML, CSS, and JavaScript using Vite. No prior experience with Firebase, cloud platforms, or backend development is assumed.

---

## Tools and Technologies Used

| Tool | Purpose |
| --- | --- |
| [MkDocs Material](https://squidfunk.github.io/mkdocs-material/) | Static site generator used to build and host the documentation |
| [GitHub Pages](https://pages.github.com/) | Hosting platform for the live documentation site |
| [Google Firebase](https://firebase.google.com/) | The software being documented (Firestore, Authentication, Hosting) |
| [VS Code](https://code.visualstudio.com/) | Code editor used for writing all Markdown files |
| [Git & GitHub](https://github.com/) | Version control and collaboration between team members |
| Markdown | Markup language used for all documentation content |
| YAML | Configuration language used for `mkdocs.yml` site settings |

---

## Our Process

### 1. Software Selection and Task Planning

We chose Google Firebase because it is the platform used in COMP 1800 for hosting, database, and authentication. We identified four distinct tasks that a new student would need to complete, each complex enough to require detailed step-by-step instructions.

### 2. Task Walkthroughs

Before writing any documentation, we each performed the Firebase setup tasks from scratch on our own machines. We recorded every click, every screen we saw, and every decision point. This ensured we did not skip steps that felt obvious to us but would not be obvious to a new student.

### 3. Writing the Documentation

We split the work between two writers:

- **Jameel Mohammed** — Task 1 (Firebase Setup), Task 2 (Firestore Setup), Introduction, Troubleshooting,
- **Julio Cesar Filho Arantes** — Task 3 (Authentication), Task 4 (Deployment), Glossary

We established a shared style guide in the Introduction (typographical conventions, admonitions, heading structure) and followed it consistently across all pages.

### 4. MkDocs Material Configuration

We used MkDocs Material for the documentation site, configuring it with:

- **Admonitions** (`pymdownx.details`, `admonition`) for notes, warnings, dangers, and success confirmations
- **Code highlighting** (`pymdownx.highlight`) with copy buttons for all code blocks
- **Tabbed content** (`pymdownx.tabbed`) for Windows/macOS keyboard shortcut differences
- **Keyboard keys** (`pymdownx.keys`) for rendering key combinations like ++ctrl+shift+j++
- **Navigation features** including instant page loading, scroll tracking, next/previous page buttons, and table of contents integration

### 5. Consistency Review

After writing, we reviewed each other's pages to ensure:

- All steps use imperative (command) verbs consistently
- Steps are separated from feedback statements and informational notes
- Admonitions are placed before the step they relate to
- Glossary terms are linked from every task page where they first appear
- Troubleshooting entries are linked inline from the relevant warning or error context
- All code uses the Firebase v9 modular SDK with Vite (no v8 CDN references)

### 6. Peer Testing

We had classmates test the instructions in lab to identify:

- Steps that were unclear or missing
- Screenshots that needed to be added or cropped
- Terminology that needed glossary definitions
- Errors that needed troubleshooting entries

Feedback was incorporated before final submission.

---

## Repository Structure

```
MKDOCS/
├── docs/
│   ├── assets/              # Screenshots and images
│   ├── index.md             # Introduction page
│   ├── task1_firebase_setup.md
│   ├── task2_firestore_setup.md
│   ├── task3_authentication.md
│   ├── task4_deploy.md
│   ├── troubleshooting.md
│   └── glossary.md
├── mkdocs.yml               # MkDocs Material configuration
└── README.md                # This file
```

---

## How to Build Locally

If you want to run this documentation site on your own machine:

1. Install Python 3 and pip.
2. Install MkDocs Material:

    ```bash
    pip install mkdocs-material
    ```

3. Clone this repository:

    ```bash
    git clone https://github.com/jameeel01/MKDOCS.git
    cd MKDOCS
    ```

4. Start the local development server:

    ```bash
    mkdocs serve
    ```

5. Open `http://127.0.0.1:8000` in your browser.

---

## Authors

- **Jameel Mohammed** — [GitHub](https://github.com/jameeel01)
- **Julio Cesar Filho Arantes** - [GitHub](https://github.com/CaesarSaladd)

BCIT CST — COMM 2216, Term 2, 2026