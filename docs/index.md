# Home

## Introduction

The purpose of this guide is to help you set up [Google Firebase](https://firebase.google.com/) for your COMP 1800 project. Firebase is a cloud platform by Google that provides tools for hosting web applications, storing data in real-time databases, and managing user authentication — all without needing to build your own backend server.

In the CST program, you will use Firebase to deploy your COMP 1800 team project so it is accessible as a live website. This guide walks you through the full setup process, from creating a Firebase project to deploying your finished application.

If you are interested in more information about Firebase's full feature set, please visit the [official Firebase documentation](https://firebase.google.com/docs).

## Is This Guide for You?

This guide is written for **first-term BCIT CST students** who are building a web application using HTML, CSS, and JavaScript for COMP 1800. No prior experience with Firebase, cloud platforms, or backend development is required.

We assume you are comfortable with:

- Writing and editing HTML, CSS, and JavaScript files
- Using a code editor such as VS Code
- Basic terminal / command line navigation (e.g., `cd`, `ls`)

## By the End of This Guide, You Will Be Able To

1. Create and configure a Firebase project in the Firebase Console
2. Set up Cloud Firestore as a database for your project
3. Set up Firebase Authentication for user login
4. Deploy your COMP 1800 project to Firebase Hosting as a live website

## Prerequisites

Before starting these instructions, make sure you have the following:

- A **Google account** (any Gmail account will work)
- **VS Code** installed on your computer ([download here](https://code.visualstudio.com/))
- **Node.js** (version 16 or higher) installed on your computer ([download here](https://nodejs.org/))
- A working **COMP 1800 project** with at least an `index.html` file
- **Google Chrome** browser (recommended for testing)

!!! note
    To check if Node.js is installed, open your terminal and type `node -v`. If a version number appears (e.g., `v18.17.0`), you are ready to proceed. If not, download and install Node.js from the link above before continuing.

## Typographical Conventions

These instructions use the following typographic conventions:

| Convention | Examples |
| --- | --- |
| **Bold text** indicates commands or actions you need to perform. | **Click**, **Enter**, **Type**, **Open**, **Select**, **Navigate** |
| `Code formatting` indicates terminal commands, file names, or code you need to type. | `npm install`, `index.html`, `firebase.firestore()` |
| [Square brackets] indicate buttons, menus, or UI elements on screen. | [Add project], [Continue], [Create database] |
| [Menu] → [Submenu] indicates a sequence of clicks through menus or navigation. | [Build] → [Firestore Database] |

## Admonitions

This guide uses the following message boxes to provide additional information:

!!! note
    **Note** provides additional helpful information related to a step. Skipping a note will not cause errors, but reading it may save you time or clarify something.

!!! warning
    **Warning** indicates an action that could cause errors, data loss, or broken configuration if ignored. Always read warnings before performing the step they are attached to.

!!! danger
    **Danger** indicates an action that could cause serious, potentially irreversible consequences such as unexpected billing charges or permanent data loss.

!!! success
    **Success** confirms the expected outcome after completing a set of steps. Use these to verify you are on the right track.