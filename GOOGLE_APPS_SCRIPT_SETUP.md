# How to Set Up "Native" Email Sending with Google Workspace

Since your website is hosted on **GitHub Pages** (which is a "static" host), it cannot send emails by itself. It needs a "backend" to talk to the email servers.

Because you use **Google Workspace**, the best "native" solution is to use **Google Apps Script**. This allows you to create a tiny, free "backend" script that lives in your Google Drive.

**This method is:**
- **Free** (included in your Google Workspace)
- **Secure** (uses your Google credentials safely)
- **Private** (no third-party service like FormSubmit.co reads your emails)

---

## Step 1: Create the Google Script

1.  Log in to your Google account (`admin@researchpathway.co.nz`).
2.  Go to [script.google.com](https://script.google.com/).
3.  Click **+ New Project**.
4.  Rename the project (click "Untitled project" at top left) to `Website Contact Form`.
5.  Delete any code in the editor (`function myFunction()...`) and paste the following code:

```javascript
// Change this to the email address where you want to receive messages
var TO_ADDRESS = "admin@researchpathway.co.nz";

function doPost(e) {
  try {
    var data = e.parameter;
    var name = data.name;
    var email = data.email;
    var program = data.program;
    var message = data.message;
    var subject = "New Contact Form Submission: " + name;

    var emailBody = "You have received a new message from your website contact form.\n\n" +
                    "Name: " + name + "\n" +
                    "Email: " + email + "\n" +
                    "Program: " + program + "\n" +
                    "--------------------------------------------------\n\n" +
                    "Message:\n" + message;

    // Send the email
    GmailApp.sendEmail(TO_ADDRESS, subject, emailBody, {
      replyTo: email
    });

    return ContentService.createTextOutput(JSON.stringify({"result":"success"}))
      .setMimeType(ContentService.MimeType.JSON);

  } catch (error) {
    return ContentService.createTextOutput(JSON.stringify({"result":"error", "error": error.toString()}))
      .setMimeType(ContentService.MimeType.JSON);
  }
}
```

6.  Press `Cmd + S` (Mac) or `Ctrl + S` to **Save**.

---

## Step 2: Deploy the Script

1.  Click the blue **Deploy** button (top right) -> **New deployment**.
2.  Click the **Select type** (gear icon) -> **Web app**.
3.  Fill in the details:
    *   **Description**: Contact Form Backend
    *   **Execute as**: `Me` (your email address)
    *   **Who has access**: **Anyone** (This is crucial so the website can send data to it).
4.  Click **Deploy**.
5.  **Authorize Access**:
    *   It will ask for permission to send emails as you.
    *   Click "Review permissions".
    *   Choose your account.
    *   *Note: You might see a "Google hasn't verified this app" warning (since you just wrote it).*
    *   Click **Advanced** -> **Go to Website Contact Form (unsafe)**.
    *   Click **Allow**.
6.  Copy the **Web App URL**. It will look like:
    `https://script.google.com/macros/s/AKfycbx.../exec`

---

## Step 3: Update Your Website

Once you have the **Web App URL**, tell me (or update the code):

1.  Open `website/contact.html`.
2.  Find the `<form>` tag.
3.  Change `action` to your new Web App URL.
4.  Add some JavaScript to handle the sending (I can provide this code once you are ready).

---

## Troubleshooting: "Emails go to Spam"

Because the script sends emails **from** your account **to** your account (which looks like a "spoofed" or "loop" email to Google's filters), they often land in Spam.

**To fix this permanently:**

1.  Open Gmail (`admin@researchpathway.co.nz`).
2.  Click the **Settings gear** -> **See all settings**.
3.  Go to the **Filters and Blocked Addresses** tab.
4.  Click **Create a new filter**.
5.  In the "Has the words" field, type:
    `"New Contact Form Submission"`
6.  Click **Create filter**.
7.  Check **Never send it to Spam**.
8.  (Optional) Check **Apply the label** -> Choose "Website Inquiries" (so they are organized!).
9.  Click **Create filter**.

Now, all future form submissions will land safely in your Inbox.
