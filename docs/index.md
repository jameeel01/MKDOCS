# Home

## Introduction

The purpose of this guide is to help you set up [Google Firebase](https://firebase.google.com/) for your COMP 1800 project. [Firebase](glossary.md#firebase) is a cloud platform by Google that provides tools for hosting web applications, storing data in real-time databases, and managing user authentication — all without needing to build your own backend server.

In the CST program, you will use Firebase to deploy your COMP 1800 team project so it is accessible as a live website. This guide walks you through the full setup process, from creating a Firebase project to deploying your finished application.

If you are interested in more information about Firebase's full feature set, please visit the [official Firebase documentation](https://firebase.google.com/docs).

## User Demographic

This guide is written for **first-term BCIT CST students** who are building a web application using HTML, CSS, and JavaScript for COMP 1800. No prior experience with Firebase, cloud platforms, or backend development is required.

## Pre-requisite Knowledge

You can perform the following tasks without assistance:

- Open, edit, and save HTML, CSS, and JavaScript files in [VS Code](https://code.visualstudio.com/)
- Navigate between folders in a terminal using commands such as `cd` and `ls` (macOS/Linux) or `cd` and `dir` (Windows)
- Open a web browser and use the address bar to visit a URL
- Copy and paste text between applications

## By the End of This Guide, You Will Be Able To

1. [Set up a Firebase project in the Firebase Console](task1_firebase_setup.md)
2. [Set up Cloud Firestore as a database for your project](task2_firestore_setup.md)
3. [Set up Firebase Authentication for user login](task3_authentication.md)
4. [Deploy your COMP 1800 project to Firebase Hosting as a live website](task4_deploy.md)

## Prerequisites

Before starting these instructions, make sure you have the following installed and ready:

- A **Google account** (any Gmail account will work)
- **[VS Code](https://code.visualstudio.com/)** installed on your computer — this is the code editor used throughout these instructions
- **[Node.js](https://nodejs.org/)** (version 16 or higher) installed on your computer — required by [Vite](glossary.md#vite) and the Firebase CLI
- A working **COMP 1800 [Vite](glossary.md#vite) project** with a `package.json`, a `src/` folder, and at least an `index.html` file — your project must be runnable with `npm run dev`
- **[Google Chrome](https://www.google.com/chrome/)** browser — recommended because these instructions reference Chrome's developer tools for testing

!!! note "Checking Node.js"
    To check if Node.js is installed, open your terminal and type `node -v`. If a version number appears (e.g., `v18.17.0`), you are ready to proceed. If not, download and install Node.js from the link above before continuing. We assume your instructor has provided you with instructions to set up and install node.js and vite. 
    

## Typographical Conventions

These instructions use the following typographic conventions:

| Convention | Examples |
| --- | --- |
| **Bold text** indicates commands or actions you need to perform. | **Click**, **Enter**, **Type**, **Open**, **Select**, **Navigate** |
| `Code formatting` indicates terminal commands, file names, or code you need to type. | `npm install`, `firebaseConfig.js`, `getFirestore()` |
| [Square brackets] indicate buttons, menus, or UI elements on screen. | [Add project], [Continue], [Create database] |
| [Menu] → [Submenu] indicates a sequence of clicks through menus or navigation. | [Build] → [Firestore Database] |

## Admonitions

This guide uses the following message boxes to provide additional information. Admonitions are always placed **before** the step they relate to. Read them before performing the action that follows.

!!! note
    **Note** provides additional helpful information related to a step. Skipping a note will not cause errors, but reading it may save you time or clarify something.

!!! warning
    **Warning** indicates an action that could cause errors, data loss, or broken configuration if ignored. Always read warnings before performing the step they are attached to.

!!! danger
    **Danger** indicates an action that could cause serious, potentially irreversible consequences such as unexpected billing charges or permanent data loss.

!!! success
    **Success** confirms the expected outcome after completing a set of steps. Use these to verify you are on the right track.