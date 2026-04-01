# Setting up Firestore Database

## Overview

This section walks you through creating a Cloud Firestore database, understanding how Firestore organizes data, adding data manually through the Firebase Console, and reading and writing data from your COMP 1800 project using JavaScript.

By the end of this page, your project will be able to store and retrieve data from a cloud database.

!!! note
    Make sure you have completed [Task 1: Initial Firebase Setup](task1_firebase_setup.md) before starting this section. Your project must already be connected to Firebase.

---

## Creating a Firestore Database

Cloud Firestore is Firebase's flexible, scalable database. You will use it to store data such as user profiles, app content, and settings for your COMP 1800 project.

1. **Open** the [Firebase Console](https://console.firebase.google.com) and **click** on your project name to open it.

2. **Click** [Databases & Storage] in the left sidebar menu.

    A submenu expands below the Build heading.

    <!-- SCREENSHOT: Left sidebar with [Databases and Storage] expanded showing submenu items including Firestore. Highlight the sidebar area. -->
    ![Firebase sidebar with Databases and Storage menu expanded](assets/firestore_setup_1.png "Databases & Storage submenu in Firebase Console")
    *Figure 1: The Databases & Storage submenu in the left sidebar.*

3. **Click** [Firestore].

    The Firestore landing page appears with a "Create database" button.

    <!-- SCREENSHOT: Firestore landing page showing the "Create database" button in the center. -->
    ![Firestore landing page with Create database button](assets/firestore_setup_2.png "Firestore Database landing page")
    *Figure 2: The Firestore Database landing page.*

4. **Click** [Create database].

    A setup wizard opens.

5. **Select** Standard Edition.

6. **Click** [Next].

7. **Select** a Firestore location from the dropdown menu. **Choose** `northamerica-northeast1 (Montréal)` as it is the closest region to Vancouver.

    !!! danger
        The database location **cannot be changed** after creation. Make sure you select the correct region before proceeding. Choosing a distant region will increase data retrieval times for your users.

    <!-- SCREENSHOT: Location dropdown with "us-west1 (Oregon)" selected or highlighted. -->
    ![Firestore location selection dropdown](assets/firestore_setup_3.png "Selecting Firestore database location")
    *Figure 3: Selecting the Oregon database location.*

8. **Click** [Next].

9. **Select** "Start in test mode."

    Test mode allows open read and write access for 30 days, which is suitable for development.

    !!! warning
        Test mode security rules expire after 30 days. If your database reads and writes suddenly stop working later in the term, check whether your security rules have expired by visiting [Firestore] → [Rules] in the Firebase Console.

    !!! note
        The Firebase Console will display the exact expiry date for your test mode rules. Take note of this date.

    <!-- SCREENSHOT: Security rules screen with "Start in test mode" radio button selected, showing the expiry date text. -->
    ![Security rules screen with test mode selected](assets/firestore_setup_4.png "Start in test mode selected")
    *Figure 4: Selecting test mode for security rules.*

10. **Click** [Create].

    Firestore takes a few seconds to provision your database. Once complete, the Firestore data viewer appears. It will be empty.

    <!-- SCREENSHOT: Empty Firestore data viewer showing the "Start collection" prompt in the center. -->
    ![Empty Firestore data viewer](assets/firestore_setup_5.png "Empty Firestore data viewer")
    *Figure 5: The empty Firestore data viewer, ready for data.*

!!! success
    You have created a Cloud Firestore database. The data viewer is now visible and ready for you to add collections and documents.

---

## Understanding Firestore Structure

Before adding data, it is important to understand how Firestore organizes information. Firestore does not use traditional tables and rows like SQL databases. Instead, it uses **collections** and **documents**.

- A **collection** is a group of documents, similar to a folder. For example, a collection called `users` would hold all user-related documents.
- A **document** is a single record within a collection, similar to a file inside a folder. Each document contains **fields** with values. For example, a document inside `users` might have fields like `name`, `email`, and `city`.
- Each document is identified by a unique **document ID**, which can be auto-generated or manually set.

Here is a visual example of how COMP 1800 project data might be organized:

```
users (collection)
├── user001 (document)
│   ├── name: "Alice"
│   ├── email: "alice@bcit.ca"
│   └── city: "Vancouver"
├── user002 (document)
│   ├── name: "Bob"
│   ├── email: "bob@bcit.ca"
│   └── city: "Burnaby"
```

!!! note
    Think of collections as tables and documents as rows if you are familiar with databases. The key difference is that each document can have different fields — they do not all need to follow the same structure.

---

## Adding Data Manually via the Firebase Console

Before writing JavaScript code, you will add a test document using the Firebase Console to confirm your database is working.

1. From the Firestore data viewer, **click** [Start collection].

    <!-- SCREENSHOT: Firestore viewer with the "Start collection" link/button highlighted. -->
    ![Start collection button in Firestore](assets/firestore_setup_6.png "Start collection button")
    *Figure 6: The Start collection button.*

2. **Enter** `users` as the Collection ID.

    <!-- SCREENSHOT: The "Start a collection" dialog with "users" typed in the Collection ID field. -->
    ![Collection ID dialog with users entered](assets/firestore_setup_7.png  "Entering the Collection ID")
    *Figure 7: Entering the collection name.*

3. **Click** [Next].

    The "Add a document" panel appears.

4. **Click** [Auto-ID] to let Firebase generate a unique document ID automatically.

    !!! note
        Auto-generated IDs look like a random string of characters (e.g., `aB3dEf7gHi`). This is normal. You can also enter a custom ID if you prefer, but Auto-ID is recommended for most cases.

5. **Enter** the first field:
    - Field name: `name`
    - Type: **select** `string` from the dropdown
    - Value: `Test User`

6. **Click** the **+** (add field) button to add another field:
    - Field name: `email`
    - Type: **select** `string`
    - Value: `testuser@bcit.ca`

7. **Click** the **+** (add field) button one more time to add a third field:
    - Field name: `city`
    - Type: **select** `string`
    - Value: `Vancouver`

    <!-- SCREENSHOT: The "Add a document" panel showing all three fields filled in (name, email, city) with the Auto-ID generated. -->
    ![Add a document panel with three fields filled in](assets/firestore_setup_8.png  "Adding a document with fields")
    *Figure 8: A completed document ready to save.*

8. **Click** [Save].

    The document now appears in the Firestore data viewer under the `users` collection.

    <!-- SCREENSHOT: Firestore data viewer showing the "users" collection with the newly created document and its fields visible. -->
    ![Firestore viewer showing the new document](assets/firestore_setup_9.png "Saved document in Firestore")
    *Figure 9: The saved document visible in the Firestore data viewer.*

!!! success
    You have manually added a document to Firestore. The `users` collection now contains one document with `name`, `email`, and `city` fields.

---

## Reading Firestore Data from Your Project

Now that there is data in your Firestore database, you will write JavaScript to retrieve and display it in the browser console.

1. **Open** your COMP 1800 project in VS Code.

2. **Create** a new file in your `scripts/` folder and **name** it `firestore_test.js`.

3. **Add** the following code to `firestore_test.js`:

    ```javascript
    // Initialize Firestore
    const db = firebase.firestore();

    // Read all documents from the "users" collection
    db.collection("users").get().then((querySnapshot) => {
        querySnapshot.forEach((doc) => {
            console.log(doc.id, " => ", doc.data());
        });
    }).catch((error) => {
        console.error("Error reading documents: ", error);
    });
    ```

    This code connects to Firestore, fetches every document in the `users` collection, and prints each document's ID and data to the browser console.

4. **Open** `index.html` in VS Code.

5. **Add** a `<script>` tag linking to your new test file. Place it **after** your Firebase configuration script and **before** the closing `</body>` tag:

    ```html
    <script src="./scripts/firestore_test.js"></script>
    ```

    !!! warning
        The `firestore_test.js` script must be loaded **after** both the Firebase SDK scripts and your `firebaseAPI_TEAMXX.js` file. If it loads before them, Firebase will not be initialized and you will see a `firebase is not defined` error.

6. **Save** both files.

7. **Open** `index.html` in Google Chrome.

8. **Open** the browser developer console:

    === "Windows"

        **Press** ++f12++ or ++ctrl+shift+j++.

    === "macOS"

        **Press** ++cmd+option+j++.

    At this point, the console should display the document ID and data you added earlier. It will look similar to:

    ```
    aB3dEf7gHi  =>  {name: "Test User", email: "testuser@bcit.ca", city: "Vancouver"}
    ```

    <!-- SCREENSHOT: Chrome DevTools console showing the Firestore read output with the document ID and fields printed. -->
    ![Console output showing Firestore data](images/placeholder_read_output.png "Firestore read output in Chrome console")
    *Figure 10: Firestore data successfully read and displayed in the console.*

!!! success
    Your project can now read data from Firestore. If you see your document data printed in the console, the connection is working correctly.

---

## Writing Data to Firestore from Your Project

Next, you will add JavaScript code that writes a new document to Firestore directly from your project.

1. **Open** `firestore_test.js` in VS Code.

2. **Add** the following code **below** the existing read code:

    ```javascript
    // Write a new document to the "users" collection
    db.collection("users").add({
        name: "Jane Doe",
        email: "janedoe@bcit.ca",
        city: "Surrey"
    }).then((docRef) => {
        console.log("Document written with ID: ", docRef.id);
    }).catch((error) => {
        console.error("Error adding document: ", error);
    });
    ```

    This code creates a new document in the `users` collection with three fields: `name`, `email`, and `city`. Firebase automatically generates a unique document ID.

3. **Save** the file.

4. **Refresh** `index.html` in Google Chrome.

5. **Open** the browser developer console (if not already open):

    === "Windows"

        **Press** ++f12++ or ++ctrl+shift+j++.

    === "macOS"

        **Press** ++cmd+option+j++.

    The console should display a message similar to:

    ```
    Document written with ID: xY9zAb2CdE
    ```

    <!-- SCREENSHOT: Chrome DevTools console showing the "Document written with ID: ..." success message. -->
    ![Console showing successful document write](assets/firestore_setup_10.png"Firestore write confirmation in console")
    *Figure 11: Confirmation that a new document was written to Firestore.*

6. **Return** to the Firebase Console in your browser.

7. **Navigate** to [Firestore Database] and **click** on the `users` collection.

8. **Verify** that the new document appears in the data viewer with the fields `name: "Jane Doe"`, `email: "janedoe@bcit.ca"`, and `city: "Surrey"`.

    <!-- SCREENSHOT: Firestore data viewer showing two documents in the "users" collection — the original test document and the newly written "Jane Doe" document. -->
    ![Firestore viewer showing two documents](assets/firestore_setup_11.png "Two documents in the users collection")
    *Figure 12: The users collection now contains two documents.*

!!! success
    Your project can now both read from and write to Firestore. You have a fully functional database connection.

---

## Cleaning Up Test Code

Before continuing to the next task, remove the test code so it does not run every time your page loads.

1. **Open** `firestore_test.js` in VS Code.

2. **Delete** all the code inside the file, or **delete** the file entirely.

3. **Open** `index.html` and **remove** the `<script>` tag that linked to `firestore_test.js`.

4. **Save** all modified files.

!!! note
    The test document you added to Firestore through the console and the document written by your JavaScript code will remain in the database. You can delete them manually from the Firestore data viewer by clicking the three-dot menu next to each document and selecting [Delete document].

---

## Conclusion

In this section, you:

- Created a Cloud Firestore database in the Firebase Console
- Learned how Firestore organizes data using collections and documents
- Added a test document manually through the Firebase Console
- Read Firestore data from your project using JavaScript and displayed it in the browser console
- Wrote a new document to Firestore from your project using JavaScript
- Cleaned up test code

If both the read and write operations displayed the expected output in the browser console, your Firestore database is correctly configured. If you encountered errors, refer to the [Troubleshooting](troubleshooting.md) page.

**Next:** Setting Up Firebase Authentication (Task 3)