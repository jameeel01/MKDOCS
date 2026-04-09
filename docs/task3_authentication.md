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

2. **Click** [Search] in the left sidebar, then search for [Authentication].
 
3. **Click** [Get started].
 
4. **Click** the [Sign-in method] tab.
 
5. **Click** [Email/Password] under the "Native providers" section.
 
    ![Sign-in method tab showing the Email/Password provider](assets/firebase_authentication_1.png "Email/Password sign-in provider")
    *Figure 1: The Email/Password provider in the Sign-in method tab.*

6. **Toggle** on the first switch labelled "Email/Password".
 
    !!! note
        Do **not** enable the second toggle labelled "Email link (passwordless sign-in)." Your COMP 1800 project will use standard password-based login only.
 
    ![Email/Password configuration panel with the top toggle enabled](assets/firebase_authentication_2.png "Enabling Email/Password authentication")
    *Figure 2: Enabling the Email/Password sign-in method.*
 
7. **Click** [Save].
 
    At this point, "Email/Password" appears as an **Enabled** provider in the list.
 
!!! success
    Email/Password authentication is now enabled for your Firebase project.
 
---
