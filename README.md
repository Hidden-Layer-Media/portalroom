# Portal Room

> *A minimalist social link aggregator — where links are shared, curated, and remembered.*

A real-time, full-stack social platform built for the quiet web. Powered by **Firebase** for centralized data, authentication, and real-time updates.

---

## 🌟 What is Portal Room?

Portal Room is a retro-inspired social platform where users can:

- **Submit links** with titles, descriptions, and tags
- **Comment on links** in real-time
- **Vote on links** (upvote/downvote) to rank content
- **Create curated lists** of related links
- **View public and personal dashboards**
- **Search and filter** links by keywords and tags
- **Real-time updates**: See new posts and comments instantly without refreshing

---

## ✨ Features

| Feature | Description |
|--------|-------------|
| **User Accounts** | Secure registration and login powered by **Firebase Auth** |
| **Authentication** | Protected pages with session management |
| **Centralized Data** | All data is stored in **Cloud Firestore** |
| **Real-time Sync** | Instant updates for new posts and comments across all users |
| **Link Submission** | Submit URLs with title, description, and tags |
| **Link Management** | Edit and delete your own links |
| **Comments** | Add, view, and delete comments on any link |
| **Voting System** | Upvote/downvote links to surface the best content |
| **Link Lists** | Create custom collections and add links to them |
| **Search** | Real-time search across titles, descriptions, and tags |
| **Mobile Responsive** | Fully optimized for mobile devices |
| **Modern Stack** | Vanilla HTML5, CSS3, JS + Firebase Backend |

---

## 📁 File Structure

```
portalroom/
├── index.html             # Homepage: latest links (public)
├── login.html             # User login (email-based)
├── register.html          # New user registration
├── dashboard.html         # Logged-in feed with search
├── submit.html            # Form to submit new links
├── profile.html           # View your links, lists, and manage data
├── list.html              # Create a new link list
├── css/
│   └── style.css          # Responsive, modern styling
├── js/
│   └── app.js             # Core logic integrated with Firebase
└── README.md              # This file
```

---

## 🚀 How to Deploy

### 1. Firebase Setup

1. Create a project at [console.firebase.google.com](https://console.firebase.google.com).
2. Enable **Authentication** (Email/Password provider).
3. Enable **Cloud Firestore** and set your Security Rules:
   ```javascript
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /profiles/{uid} {
         allow read: if true;
         allow write: if request.auth != null && request.auth.uid == uid;
       }
       match /posts/{postId} {
         allow read: if true;
         allow create: if request.auth != null;
         allow update, delete: if request.auth != null && request.auth.uid == resource.data.user_id;
         
         match /comments/{commentId} {
           allow read: if true;
           allow create: if request.auth != null;
           allow delete: if request.auth != null && request.auth.uid == resource.data.user_id;
         }
         
         match /votes/{userId} {
           allow read: if true;
           allow write: if request.auth != null && request.auth.uid == userId;
         }
       }
     }
   }
   ```
4. Create a **Web App** in your Firebase project and copy the `firebaseConfig` object.
5. Open `js/app.js` and replace the `firebaseConfig` block at the top with your credentials.

### 2. Static Hosting (GitHub Pages)

1. **Fork or clone** this repo.
2. Go to **Settings → Pages**.
3. Set **Source** to your branch (e.g., `main`) → `/ (root)`.
4. Click **Save**.
5. Your site will be live at `https://YOURUSERNAME.github.io/portalroom`.

---

## 💾 How User Data Works

- **Centralized**: All data is shared across all users globally.
- **Secure**: Authentication and Firestore Security Rules ensure users can only modify their own content.
- **Real-time**: Firebase Firestore listeners keep the feed "alive" without manual refreshes.

---

## 📝 License

MIT — Do whatever you want with this.
Modify it. Break it. Make it yours.

---

## 🤝 Contributing

Portal Room is intentionally minimal, but contributions are welcome:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

---

## 📊 Technical Stack

- **Frontend**: Vanilla HTML5, CSS3, JavaScript (ES6+)
- **Backend**: Firebase (Firestore, Auth)
- **Deployment**: GitHub Pages (or any static host)

---

> *"I don't want to be famous. I just want to leave something behind."*
> — Portal Room

**Version**: 2.1.0 (Firebase Edition)
**Status**: Ready for Backend Configuration ✅
