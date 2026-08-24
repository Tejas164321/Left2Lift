# 🌿 Left2Lift
 
> **Connecting food donors and NGOs to reduce food waste and power last-mile food redistribution.**
 
![React](https://img.shields.io/badge/React_18-20232A?style=flat-square&logo=react&logoColor=61DAFB)
![TypeScript](https://img.shields.io/badge/TypeScript-007ACC?style=flat-square&logo=typescript&logoColor=white)
![Vite](https://img.shields.io/badge/Vite_5-646CFF?style=flat-square&logo=vite&logoColor=white)
![Firebase](https://img.shields.io/badge/Firebase-FFCA28?style=flat-square&logo=firebase&logoColor=black)
![TailwindCSS](https://img.shields.io/badge/Tailwind_CSS-38B2AC?style=flat-square&logo=tailwind-css&logoColor=white)
![Google Maps](https://img.shields.io/badge/Google_Maps_API-4285F4?style=flat-square&logo=googlemaps&logoColor=white)
![React Router](https://img.shields.io/badge/React_Router_7-CA4245?style=flat-square&logo=react-router&logoColor=white)
![MIT License](https://img.shields.io/badge/License-MIT-green?style=flat-square)
 
---
 
## 📌 Table of Contents
 
- [Overview](#-overview)
- [How It Works](#-how-it-works)
- [Implemented Features](#-implemented-features)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Getting Started](#-getting-started)
- [Environment Variables](#-environment-variables)
- [Available Scripts](#-available-scripts)
- [Data Model (Firestore)](#-data-model-firestore)
- [Notes](#-notes)
- [License](#-license)
---
 
## 🌍 Overview.
 
**Left2Lift** is a role-based web app built to eliminate food waste at the last mile.
 
| Role | Who | What they do |
|------|-----|--------------|
| 🍽️ **Donor** | Restaurants, events, caterers | Post surplus food pickups with location & time details |
| 🤝 **NGO** | Non-profit organizations | Discover nearby donations, claim them, and navigate to pickups |
 
The platform provides real-time updates, map-based discovery, and route optimization — making food redistribution fast and transparent.
 
---
 
## 🔄 How It Works
 
```
1. Donor signs in → posts a new food donation
         ↓
2. Donation saved to Firestore  (status: available)
         ↓
3. NGO dashboard receives real-time update
         ↓
4. NGO claims a donation  (status: claimed)
         ↓
5. NGO navigates using in-app map route tools
         ↓
6. Pickup completed and marked done  (status: picked)
```
 
---
 
## ✨ Implemented Features.
 
### 🔐 Authentication & Roles
- Email/password sign-up and login via **Firebase Authentication**
- Role selection during signup: **donor** or **ngo**
- Role-based routing:
  - `/donor` → Donor dashboard
  - `/ngo` → NGO dashboard
---
 
### 🍽️ Donor Features
- Post a donation with:
  - Title, description, quantity, and food type
  - Best-before datetime and pickup window
  - Address + GPS coordinates
- **Google Places Autocomplete** for address input
- Browser **geolocation auto-fill** as fallback
- Donor dashboard with live status summary cards:
  - Total · Available · Claimed · Completed
---
 
### 🤝 NGO Features
- **Real-time donation feed** powered by Firestore listeners
- Toggle between **Map View** and **List View**
- Smart filters: `All Available` · `Available Now` · `Claimed` · `Mine`
- One-click claim flow with instant Firestore status sync
- **Quick open route** in Google Maps (`maps/dir` → fallback to `maps/search`)
- Live map markers with donation info windows
- **Multi-pickup route planner:**
  - Optimized waypoints via Google Directions API
  - ETA + distance display
  - Step-by-step progress tracking and completion flow
- In-app **notifications** when new donations are posted
---
 
### 🎨 UI / UX
- Fully responsive dashboards for donor and NGO roles
- Status-aware donation cards with color-coded badges
- Modal-based posting and route flows
- Clean design powered by Tailwind CSS + Lucide icons
---
 
## 🛠️ Tech Stack
 
| Layer | Technology |
|-------|-----------|
| ⚛️ **Frontend** | React 18 + TypeScript |
| ⚡ **Build Tool** | Vite 5 |
| 🔀 **Routing** | React Router DOM 7 |
| 🎨 **Styling** | Tailwind CSS |
| 🖼️ **Icons** | Lucide React |
| 🔐 **Authentication** | Firebase Authentication |
| 🗄️ **Database** | Cloud Firestore (real-time) |
| 📦 **Storage** | Firebase Storage |
| 🗺️ **Maps** | Google Maps JS API — Maps · Places · Directions · Geometry |
 
---
 
## 📂 Project Structure
 
```
Left2Lift/
├── public/
├── src/
│   ├── components/
│   │   ├── Auth/               # Login, Signup, Role selection
│   │   ├── Donor/              # Donor dashboard & post-donation forms
│   │   ├── NGO/                # NGO feed, map view, route planner
│   │   └── Layout/             # Shared layout wrappers, navbar
│   ├── config/
│   │   └── firebase.ts         # Firebase app initialization
│   ├── hooks/
│   │   ├── useAuth.ts          # Auth state & role management
│   │   └── useGoogleMaps.ts    # Maps API loader & helpers
│   ├── types/
│   │   └── index.ts            # Shared TypeScript interfaces
│   └── App.tsx                 # Root component & route definitions
├── .env                        # Environment variables (not committed)
├── .env.example                # Template for environment setup
├── index.html
├── package.json
├── tailwind.config.ts
├── tsconfig.json
└── vite.config.ts
```
 
---
 
## 🚀 Getting Started
 
### Prerequisites
 
- **Node.js** v18 or higher
- **npm** v9+ (or yarn / pnpm)
- A **Firebase project** → [Create one here](https://console.firebase.google.com/)
- A **Google Cloud project** with Maps APIs enabled → [Cloud Console](https://console.cloud.google.com/)
---
 
### 1) Clone the repository
```bash
git clone https://github.com/Tejas164321/Left2Lift.git
cd Left2Lift
```
 
### 2) Install dependencies
```bash
npm install
```
 
### 3) Add environment variables
```bash
cp .env.example .env
# Open .env and fill in your Firebase + Google Maps keys
```
 
### 4) Start the development server
```bash
npm run dev
```
 
Open the local URL shown by Vite — typically **`http://localhost:5173`**
 
---
 
## 🔐 Environment Variables
 
Create a `.env` file in the project root (same level as `package.json`):
 
```env
# Firebase Configuration
VITE_FIREBASE_API_KEY=your_firebase_api_key
VITE_FIREBASE_AUTH_DOMAIN=your-project-id.firebaseapp.com
VITE_FIREBASE_PROJECT_ID=your-project-id
VITE_FIREBASE_STORAGE_BUCKET=your-project-id.appspot.com
VITE_FIREBASE_MESSAGING_SENDER_ID=your_sender_id
VITE_FIREBASE_APP_ID=your_app_id
 
# Google Maps
VITE_GOOGLE_MAPS_API_KEY=your_google_maps_api_key
```
 
### Where to find these values
 
| Variable | Where to get it |
|----------|----------------|
| `VITE_FIREBASE_*` | Firebase Console → Project Settings → Your Apps → Web App SDK Config |
| `VITE_GOOGLE_MAPS_API_KEY` | Google Cloud Console → APIs & Services → Credentials → Create API Key |
 
### Required Google Maps APIs
 
Enable all of the following in your Google Cloud project:
 
- ✅ Maps JavaScript API
- ✅ Places API
- ✅ Directions API
- ✅ Geometry Library *(loaded via Maps JS API)*
> 💡 **Tip:** Restrict your API key by HTTP referrer in production to prevent unauthorized usage.
 
---
 
## 📜 Available Scripts
 
```bash
npm run dev       # Start development server with hot reload
npm run build     # Production build → outputs to dist/
npm run preview   # Preview the production build locally
npm run lint      # Run ESLint across the project
```
 
---
 
## 🧾 Data Model (Firestore)
 
### `users` collection
 
| Field | Type | Description |
|-------|------|-------------|
| `email` | `string` | User's email address |
| `displayName` | `string` | Display name |
| `role` | `"donor" \| "ngo"` | User role assigned at signup |
| `createdAt` | `timestamp` | Account creation time |
 
---
 
### `donations` collection
 
| Field | Type | Description |
|-------|------|-------------|
| `donorId` | `string` | UID of the posting donor |
| `donorName` | `string` | Display name of the donor |
| `title` | `string` | Donation title |
| `description` | `string` | Description of the food |
| `quantity` | `string` | Amount / portions available |
| `foodType` | `string` | Category (e.g. cooked, packaged) |
| `expiryTime` | `timestamp` | Best-before datetime |
| `pickupWindow` | `string` | Available pickup time range |
| `location.lat` | `number` | Latitude coordinate |
| `location.lng` | `number` | Longitude coordinate |
| `location.address` | `string` | Human-readable address |
| `status` | `"available" \| "claimed" \| "picked" \| "expired"` | Current donation status |
| `claimedBy` | `string?` | NGO UID *(set when claimed)* |
| `claimedByName` | `string?` | NGO display name *(set when claimed)* |
| `claimedAt` | `timestamp?` | Timestamp of when donation was claimed |
| `createdAt` | `timestamp` | When the donation was originally posted |
 
> ⚠️ **Firestore Indexes:** Combined `where + orderBy` queries used in dashboards may require composite indexes. Firestore will log a direct link in your browser console to create them if they are missing.
 
---
 
## 📝 Notes
 
- Some UI labels may still reference older naming (e.g. `"ZeroWaste DineMap"` text in a few places). These are cosmetic leftovers and do not affect any core functionality.
- Configure **Firestore Security Rules** before deploying to production to restrict read/write access by user role.
- The Google Maps API key should be **HTTP referrer restricted** in production environments.
---
 
## 🤝 Contributing
 
Contributions, issues, and feature requests are welcome!
 
1. Fork the repository
2. Create a feature branch → `git checkout -b feature/your-feature-name`
3. Commit your changes → `git commit -m 'feat: describe your change'`
4. Push to the branch → `git push origin feature/your-feature-name`
5. Open a Pull Request
---
 
## 📄 License
 
This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details..
 
---
 
> Made with ❤️ to reduce food waste, one pickup at a time...
> ⭐ Star this repo if you find it helpful!
