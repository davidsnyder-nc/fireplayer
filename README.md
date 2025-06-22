# Fire Player

A modern, Firebase-powered podcast and audio player application with AI-enhanced features.

## Features

- **Audio Management**: Upload and organize your personal audio files
- **RSS Feed Integration**: Import podcast episodes from RSS feeds
- **AI-Powered Enhancements**: Automatic naming and artwork generation using Gemini AI
- **Advanced Player Controls**: ±30 second skip, playback speed control, volume control
- **Visual Feedback**: Currently playing indicators with theme-aware styling
- **Responsive Design**: Optimized for both desktop and mobile devices
- **Theme Support**: Light and dark theme switching
- **Organized Collections**: Separate "My Audio" and "Podcasts" tabs with RSS feed management

## Setup Instructions

### 1. Firebase Configuration

1. Create a new Firebase project at [Firebase Console](https://console.firebase.google.com/)
2. Enable Authentication with Anonymous sign-in
3. Set up Firestore Database
4. Set up Storage
5. Copy your Firebase configuration and update `firebase-config.json`

### 2. Security Rules

**Firestore Rules:**
```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /podcasts/{document} {
      allow read, write: if request.auth != null;
    }
    match /rssFeeds/{document} {
      allow read, write: if request.auth != null;
    }
  }
}
```

**Storage Rules:**
```javascript
rules_version = '2';
service firebase.storage {
  match /b/{bucket}/o {
    match /audio/{allPaths=**} {
      allow read, write: if request.auth != null;
    }
    match /artwork/{allPaths=**} {
      allow read, write: if request.auth != null;
    }
  }
}
```

### 3. Optional: Gemini AI Integration

For AI-powered features like automatic naming and artwork generation:
1. Get a Gemini API key from [Google AI Studio](https://aistudio.google.com/app/apikey)
2. Add it to your `firebase-config.json` as `geminiApiKey`

### 4. Configuration File

Update `firebase-config.json` with your credentials:
```json
{
  "apiKey": "your-firebase-api-key",
  "authDomain": "your-project.firebaseapp.com",
  "projectId": "your-project-id",
  "storageBucket": "your-project.appspot.com",
  "messagingSenderId": "123456789012",
  "appId": "1:123456789012:web:abcdef123456789012345678",
  "geminiApiKey": "your-gemini-api-key-optional"
}
```

## Usage

1. Open the application in a web browser
2. Configure Firebase settings using the settings modal (gear icon)
3. Upload audio files or import RSS feeds
4. Enjoy your personalized audio experience!

## Technologies Used

- **Frontend**: HTML5, CSS3, JavaScript, Tailwind CSS
- **Backend**: Firebase (Firestore, Storage, Authentication)
- **AI Integration**: Google Gemini API
- **Audio**: HTML5 Audio API

## File Structure

- `index.html` - Main application file
- `firebase-config.json` - Firebase configuration (update with your credentials)
- `logo.png` - Application logo
- `README.md` - This documentation

## License

This project is open source and available under the MIT License.