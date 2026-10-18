REAL CHAT — NATIVE ANDROID PROJECT

This is a native Android Studio project (Kotlin), not a website. It is a starter group-chat app using Firebase Authentication (anonymous sign-in) and Firebase Realtime Database for live messages shared across devices.

IMPORTANT: An APK is not included because a live Firebase project must be configured and the Android project must be built and tested.

REQUIREMENTS
- Android Studio
- A Google/Firebase account
- Internet connection on phones

SETUP FIREBASE
1. Open https://console.firebase.google.com/ and create a Firebase project.
2. Add an Android app with package name: com.example.realchat
3. Download google-services.json and place it in the app/ folder (next to app/build.gradle.kts).
4. In Firebase Console > Authentication > Sign-in method, enable Anonymous.
5. In Firebase Console > Realtime Database, create a database.
6. For a private testing prototype, set these rules while testing:
{
  "rules": {
    "publicChat": {
      "messages": {
        ".read": "auth != null",
        ".write": "auth != null",
        "$messageId": {
          ".validate": "newData.hasChildren(['uid','name','text','timestamp'])",
          "uid": { ".validate": "newData.isString() && newData.val() == auth.uid" },
          "name": { ".validate": "newData.isString() && newData.val().length > 0 && newData.val().length <= 40" },
          "text": { ".validate": "newData.isString() && newData.val().length > 0 && newData.val().length <= 1000" },
          "timestamp": { ".validate": "newData.isNumber()" },
          "$other": { ".validate": false }
        }
      }
    }
  }
}
These rules are for a starter public group chat only. They allow any authenticated app user to read and post to the public room. They do not provide private conversations, robust identity verification, abuse moderation, or end-to-end encryption. Tighten rules before public release.

BUILD APK
1. Open Android Studio.
2. Choose Open and select the RealChat project folder.
3. Add app/google-services.json as described above.
4. Allow Gradle sync to finish.
5. Choose Build > Build Bundle(s) / APK(s) > Build APK(s).
6. Android Studio shows the APK output path when build finishes. Use Build > Generate Signed Bundle / APK for a release APK.

CURRENT FEATURES
- Native Android interface
- Shared live group chat across devices
- Anonymous Firebase authentication
- Display names, message timestamps, and real-time updates
- Message sending and error feedback

NOT YET INCLUDED
- Private one-to-one chats
- Push notifications when the app is closed
- Phone-number verification, profile pictures, group administration, or end-to-end encryption
