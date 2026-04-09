# Deploying Your Project to Firebase Hosting
 
## Overview
 
This section walks you through installing the Firebase CLI, logging in, building your project with Vite, and deploying to Firebase Hosting as a live website.
 
By the end of this page, your project will be publicly accessible at a `web.app` URL.
 
!!! note
    Make sure you have completed [Task 1: Initial Firebase Setup](task1_firebase_setup.md) before starting this section. Node.js version 16 or higher must be installed. To check, open your terminal and run `node -v`.
 
!!! warning
    Deploying your project makes it **publicly accessible on the internet.** Confirm that your project does not contain any private credentials in plain JavaScript files, or personal information you do not intend to share.
 
---

## Installing the Firebase CLI
 
You will need to use the Firebase CLI tool to deploy your project directly from your terminal.
 
1. **Open** the integrated terminal in VS Code:

 
2. **Type** the following command and **press** ++enter++:
 
    ```
    npm install -g firebase-tools
    ```
 
    Npm downloads and installs the Firebase CLI globally. This may take up to one minute.
 
    !!! note
        The `-g` flag installs the CLI globally so the `firebase` command is available in any project folder. You only need to run this once per computer.
 
3. **Verify** the installation by running:
 
    ```
    firebase --version
    ```
 
    The terminal should print a version number, confirming a successful install.
 
!!! success
    The Firebase CLI is installed and ready to use.

---

