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
        The command `-g` installs the CLI globally so the `firebase` command is available in any project folder. You only need to run this once per computer.
 
3. **Verify** the installation by running:
 
    ```
    firebase --version
    ```
 
    The terminal should print a version number, confirming a successful install.
 
!!! success
    The Firebase CLI is installed and ready to use.

---

## Initializing Firebase Hosting
 
1. **Confirm** your terminal is inside your project folder. 
 
2. **Run**:
 
    ```
    firebase init hosting
    ```
 
   The Firebase CLI will start an interactive setup wizard.
 
  ![Terminal showing the Firebase init hosting wizard](assets/firebase_deployement_1.png "Firebase init hosting wizard")

*Figure 2: The Firebase Hosting setup wizard.*
 
3. When prompted to "Please select an option," **select** [Use an existing project] and **press** ++enter++.
 
4. **Select** your project from the list and **press** ++enter++.
 
5. When asked "What do you want to use as your public directory?", **type** `dist` and **press** ++enter++.
 
    !!! warning
        If you do not type dist, Firebase will deploy your raw source files rather than the compiled build, and your app will not work correctly on the live URL.
 
6. When asked "Configure as a single-page app (rewrite all URLs to /index.html)?", **type** `N` and **press** ++enter++.
 
7. When asked "Set up automatic builds and deploys with GitHub?", **type** `N` and **press** ++enter++.
 
8. If asked "File dist/index.html already exists. Overwrite?", **type** `N` and **press** ++enter++.
 
    After this step, the CLI prints:
 
    ```
    ✔  Firebase initialization complete!
    ```
 
    Two files are added to your project root: `firebase.json` and `.firebaserc`.
 
!!! success
    Firebase Hosting is configured. Your `firebase.json` should look similar to this:
 
    ```json
    {
      "hosting": {
        "public": "dist",
        "ignore": [
          "firebase.json",
          "**/.*",
          "**/node_modules/**"
        ]
      }
    }
    ```
 
---

