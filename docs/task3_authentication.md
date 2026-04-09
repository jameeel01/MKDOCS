# Setting Up Firebase Authentication

## Overview

This section walks you through enabling Firebase Authentication in the Firebase Console, creating the `src/firebaseConfig.js`, `src/authentication.js`, and `src/login.js` module files, and building a single `Login.html` page with toggling login and sign-up views.

The goal of this page is to allow users to create accounts with a username and email address, sign in with email and password, and be redirected to the `Login.html` page when they visit a protected page without being signed in.

!!! note
    Make sure you have completed [Task 1: Initial Firebase Setup](task1_firebase_setup.md) 
    and [Task 2: Setting Up Cloud Firestore](task2_firestore_setup.md) 
    before starting this section. Your project must already have Firebase installed 
    as a Node package and have a working `src/firebaseConfig.js` skeleton.

!!! note
    Your COMP 1800 project will use the **Firebase v9 modular SDK** bundled through Vite, 
---

## Enabling Email/Password Authentication

Before writing any code, you must enable the Email/Password sign-in method inside the Firebase Console.

1. **Open** the [Firebase Console](https://console.firebase.google.com) and **click** on your project.

2. **Click** [Build] in the left sidebar, then **click** [Authentication].
