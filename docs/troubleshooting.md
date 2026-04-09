# Troubleshooting

This page lists common issues you may encounter while following these instructions, along with their likely causes and solutions. Each section corresponds to a specific error message or unexpected behavior.

---

## Firebase Console Issues

### "Permission denied" when accessing the Firebase Console

| | |
| --- | --- |
| **Problem** | You see a "Permission denied" or "You don't have access" message when opening the [Firebase Console](glossary.md#firebase-console). |
| **Possible Cause** | You are signed in with a different Google account than the one used to create the project. |
| **Solution** | **Click** your profile icon in the top right corner of the Firebase Console. **Verify** the correct Google account is active. If you have multiple accounts, **click** [Switch account] and **sign in** with the account you used to create the project. |

---

### Firebase project not appearing in the Console

| | |
| --- | --- |
| **Problem** | You created a Firebase project but cannot find it in the Console dashboard. |
| **Possible Cause** | The project was created under a different Google account. |
| **Solution** | **Click** the project dropdown at the top of the Firebase Console page to view all available projects. If none appear, **try** signing in with your other Google accounts. The project will only be visible to the account that created it (or accounts that have been granted access). |

---

## Firebase Connection Issues

### Firebase initialization errors in Vite

| | |
| --- | --- |
| **Problem** | The browser console shows an error such as `Failed to resolve import "firebase/app"` or `Module not found: firebase`. |
| **Possible Cause** | The Firebase npm package is not installed in your project. |
| **Solution** | **Open** the terminal in VS Code, **confirm** you are in your project folder, and **run**: |

```bash
npm install firebase
```

After installation completes, **restart** the Vite dev server with `npm run dev`.

!!! note
    If you see `Cannot find module './firebaseConfig.js'`, check that the file exists at `src/firebaseConfig.js` and that your import path is correct (e.g., `import { db } from "./firebaseConfig.js"` — the `./` and `.js` extension are both required).

---

### `src/firebaseConfig.js` not initializing correctly

| | |
| --- | --- |
| **Problem** | The browser console shows errors like `FirebaseError: Firebase: No Firebase App '[DEFAULT]' has been created` or `auth is not defined`. |
| **Possible Cause** | The configuration values in `src/firebaseConfig.js` still contain placeholders, have a typo, or the file is not exporting `db` and `auth` correctly. |
| **Solution** | **Open** `src/firebaseConfig.js` in VS Code and **check** the following: |

1. The `firebaseConfig` object contains your **actual** project values — not the `YOUR_API_KEY`, `YOUR_PROJECT_ID` placeholders.

2. The file includes all three required imports at the top:

    ```javascript
    import { initializeApp } from "firebase/app";
    import { getFirestore } from "firebase/firestore";
    import { getAuth } from "firebase/auth";
    ```

3. The file exports both instances at the bottom:

    ```javascript
    export const db   = getFirestore(app);
    export const auth = getAuth(app);
    ```

!!! warning
    Even a single incorrect character in your configuration values will prevent Firebase from initializing. If you are unsure of your values, you can find them again in the [Firebase Console](glossary.md#firebase-console) under [Project Settings] → [Your apps] → [SDK setup and configuration].

---

## Firestore Issues

### Firestore reads and writes suddenly stopped working

| | |
| --- | --- |
| **Problem** | Firestore code that was previously working now returns `PERMISSION_DENIED` errors in the browser console. |
| **Possible Cause** | Your [test mode](glossary.md#test-mode) [security rules](glossary.md#security-rules) have expired. Test mode rules only last 30 days from the date your database was created. |
| **Solution** | Follow the steps below to update your security rules. |

1. **Open** the [Firebase Console](https://console.firebase.google.com) and **navigate** to your project.

2. **Click** [Firestore Database] in the left sidebar.

3. **Click** the [Rules] tab at the top of the page.

4. **Check** the expiry date in the existing rules. If the date has passed, this is the cause of the error.

5. **Replace** the entire contents of the rules editor with the following:

    ```
    rules_version = '2';
    service cloud.firestore {
      match /databases/{database}/documents {
        match /{document=**} {
          allow read, write: if request.time < timestamp.date(2026, 8, 31);
        }
      }
    }
    ```

    !!! note
        Adjust the date (`2026, 8, 31`) to a reasonable future date that covers the rest of your COMP 1800 term. The format is `year, month, day`.

6. **Click** [Publish].

7. **Return** to your project in the browser and **refresh** the page. The `PERMISSION_DENIED` errors should now be resolved.

!!! warning
    These open rules are appropriate only for development during your COMP 1800 term. Do not use them on a production application accessible to the public.

---

### Console shows no output when reading from Firestore

| | |
| --- | --- |
| **Problem** | Your Firestore read code runs without any errors, but nothing prints to the browser console. |
| **Possible Cause** | The [collection](glossary.md#collection) is empty, the collection name is misspelled, or the test file is not being imported. |
| **Solution** | **Check** the following three things: |

1. The collection name in your JavaScript code **exactly matches** what appears in the Firebase Console. Names are case-sensitive — `users` is not the same as `Users` or `USERS`.

2. There is at least one [document](glossary.md#document) inside the collection. **Open** the [Firestore data viewer](glossary.md#firestore-data-viewer) in the Firebase Console and **verify** that the collection contains data.

3. Your test file is being imported. **Open** `src/main.js` and **confirm** it contains `import "./firestoreTest.js";`.

!!! note
    If you still see no output, **try** adding `console.log("Script loaded");` at the very top of `src/firestoreTest.js` and refreshing the page. If that message does not appear in the console, the file is not being loaded — check the import path for typos.

---

### `PERMISSION_DENIED` error when writing to Firestore

| | |
| --- | --- |
| **Problem** | The console shows `FirebaseError: Missing or insufficient permissions` when attempting to write data to Firestore. |
| **Possible Cause** | Your [security rules](glossary.md#security-rules) do not allow write access. This usually means [test mode](glossary.md#test-mode) has expired. |
| **Solution** | **Navigate** to [Firestore Database] → [Rules] in the Firebase Console. If the rules contain `allow read, write: if false;`, test mode has expired. Follow the steps in [Firestore reads and writes suddenly stopped working](#firestore-reads-and-writes-suddenly-stopped-working) above to update your rules. |

---

## Authentication Issues

### Authentication redirect loop

| | |
| --- | --- |
| **Problem** | The browser keeps redirecting between `login.html` and another page in an infinite loop, or the page freezes. |
| **Possible Cause** | The `requireLogin()` function from `src/authentication.js` is being called on `login.html` itself. |
| **Solution** | **Open** the script file loaded by `login.html` (typically `src/login.js`) and **verify** it does **not** contain `import { requireLogin }` or a call to `requireLogin()`. The `requireLogin()` function should only be imported on pages that require the user to be signed in — never on the login page itself. |

---

### "auth/weak-password" error when signing up

| | |
| --- | --- |
| **Problem** | The sign-up form shows an error containing `auth/weak-password`. |
| **Possible Cause** | Firebase requires passwords to be at least 6 characters long. |
| **Solution** | **Enter** a password that is at least 6 characters. Consider adding a note in your sign-up form HTML that informs users of this requirement. |

---

## Deployment Issues

### `npm run build` fails with errors

| | |
| --- | --- |
| **Problem** | Running `npm run build` produces errors in the terminal and does not create a `dist/` folder. |
| **Possible Cause** | Your JavaScript code contains syntax errors, missing imports, or references to files that do not exist. |
| **Solution** | **Read** the error messages in the terminal output carefully — they typically include a file name and line number. **Open** the file indicated, **fix** the error, and **run** `npm run build` again. Common causes include misspelled import paths, missing closing brackets, and importing from a file that has been renamed or deleted. |

---

### Site shows blank page or old content after deploying

| | |
| --- | --- |
| **Problem** | After running `firebase deploy --only hosting`, the live site shows a blank white page, a Firebase default page, or content that does not match your latest changes. |
| **Possible Cause** | You either forgot to run `npm run build` before deploying, or the `dist/` folder contains stale files from a previous build. |
| **Solution** | **Run** the following two commands in order, then check your live URL again: |

```bash
npm run build
firebase deploy --only hosting
```

!!! warning
    You must run `npm run build` **before every deploy**. The `firebase deploy` command uploads whatever is currently in `dist/` — if you skip the build step, it will deploy old or missing files.

---

### `firebase deploy` returns "Error: No project active"

| | |
| --- | --- |
| **Problem** | Running `firebase deploy` shows `Error: No project active` or `Error: Could not determine the project`. |
| **Possible Cause** | You have not initialized Firebase Hosting in this project folder, or the `.firebaserc` file is missing. |
| **Solution** | **Run** `firebase init hosting` and follow the setup wizard as described in [Deploying Your Project](task4_deploy.md#initializing-firebase-hosting). If you have already initialized but the error persists, **run** `firebase use --add`, **select** your project, and **try** deploying again. |