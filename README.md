# Budget Planner — Finance Dashboard with Visualizations

An interactive budgeting dashboard built with Vue 3, Chart.js, and Firebase.

## Features
- 📊 Dashboard with income/expense summary cards and charts
- 💳 Full transaction CRUD with filters (type, category, month, search)
- 🎯 Savings goals with visual progress bars and monthly contribution calculator
- 📈 Analytics view: trend lines, pie charts, bar charts, category breakdown table
- ☁️ Optional Firebase sync with Google Auth — works offline without login
- 💾 Local storage fallback when not signed in

## Tech Stack
- Vue 3 + Vite + Pinia
- Chart.js + vue-chartjs (Doughnut, Bar, Line charts)
- Firebase Auth + Firestore (optional)

  ## 📸 Project Screenshots

### 🏠 Homepage
![Homepage](./images/homepage.png)

### 📊 Dashboard
![Dashboard](./images/dashboard.png)

### 📈 Analytics
![Analytics](./images/analytics.png)

### 💸 Transaction Form
![Transaction](./images/transaction.png)

### 📑 Transaction Page
![Transaction Page](./images/transaction-page.png)

### 🎯 Goals Section
![Goals](./images/goals.png)

## Getting Started

```bash
cd budget-planner
npm install
npm run dev
```

## Firebase Setup (Optional)
1. Create a project at [Firebase Console](https://console.firebase.google.com)
2. Enable **Google Auth** and **Firestore**
3. Copy your config into `src/firebase.js`
4. Add Firestore security rules:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /transactions/{id} {
      allow read, write: if request.auth != null && request.auth.uid == resource.data.userId;
      allow create: if request.auth != null && request.auth.uid == request.resource.data.userId;
    }
    match /goals/{id} {
      allow read, write: if request.auth != null && request.auth.uid == resource.data.userId;
      allow create: if request.auth != null && request.auth.uid == request.resource.data.userId;
    }
  }
}
```

Without Firebase config, the app runs fully in offline mode using localStorage.
