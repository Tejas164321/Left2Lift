# Left2Lift

**Left2Lift connects food donors and NGOs to reduce food waste and improve last-mile food redistribution.**

---

## 📌 Table of Contents

- [Overview](#-overview)
- [Implemented Features](#-implemented-features)
- [How It Works](#-how-it-works)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Environment Variables](#-environment-variables)
- [Getting Started](#-getting-started)
- [Available Scripts](#-available-scripts)
- [Data Model (Firestore)](#-data-model-firestore)
- [Notes](#-notes)
- [License](#-license)

---

## 🌍 Overview

Left2Lift is a role-based web app where:
- **Donors** (restaurants/events) post surplus food pickups.
- **NGOs** discover nearby pickups, claim them, and navigate to locations.

The project currently uses a **Vite + React + TypeScript + Firebase** architecture with map-based donation discovery and route assistance.

---

## ✨ Implemented Features

### Authentication & Roles
- Email/password sign up and login using Firebase Authentication.
- Role selection during signup: **donor** or **ngo**.
- Role-based routing:
  - `/donor` for donors
  - `/ngo` for NGOs

### Donor Features
- Post donation with:
  - title, description, quantity, food type
  - best-before datetime
  - pickup window
  - address + coordinates
- Google Places autocomplete support in address input.
- Auto-fill fallback using browser geolocation.
- Donor dashboard with donation status cards:
  - total, available, claimed, completed.

### NGO Features
- Real-time donation feed from Firestore.
- Map and list view toggle.
- Filters: all available, available now, claimed, mine.
- Claim donation flow (status update in Firestore).
- Quick open route in Google Maps (`maps/dir` fallback to `maps/search`).
- Live map markers with donation info windows.
- Multi-pickup selector and route tracker:
  - optimized waypoints via Google Directions API
  - ETA + distance display
  - progress tracking and completion flow
- In-app notification when new donations appear.

### UI/UX
- Responsive dashboards for donor/NGO use.
- Status-aware donation cards and badges.
- Modal-based posting and route flows.

---

## 🔄 How It Works

1. Donor signs in and posts a new food donation.
2. Donation is stored in Firestore (`donations`) with status `available`.
3. NGO dashboard receives updates in real-time.
4. NGO claims a donation (`claimedBy`, `claimedByName`, `claimedAt`).
5. NGO navigates using map route tools and external Google Maps directions.
6. Pickup progress is tracked in the route experience.

---

## 🛠️ Tech Stack

- **Frontend:** React 18 + TypeScript
- **Build Tool:** Vite 5
- **Routing:** React Router DOM 7
- **Styling:** Tailwind CSS
- **Icons:** Lucide React
- **Backend Services:** Firebase
  - Authentication
  - Firestore
  - Storage
- **Maps:** Google Maps JavaScript API (Maps, Places, Geometry)

---

## 📂 Project Structure

```text
src/
  components/
    Auth/
    Donor/
    NGO/
    Layout/
  config/
    firebase.ts
  hooks/
    useAuth.ts
    useGoogleMaps.ts
  types/
    index.ts
  App.tsx
```

---

## 🔐 Environment Variables

Create a `.env` file in the project root (same level as `package.json`) with:

```env
# Firebase configuration
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
- **Firebase keys** – Firebase Console → Project Settings → Your apps → Web app SDK config.
- **Google Maps key** – [Google Cloud Console](https://console.cloud.google.com/) → APIs & Services → Credentials → Create API key.

### Required Google Maps APIs
Enable the following in the Google Cloud Console for your key:
- Maps JavaScript API
- Places API
- Directions API

---

## 🚀 Getting Started

### 1) Clone
```bash
git clone https://github.com/Tejas164321/Left2Lift.git
cd Left2Lift
```

### 2) Install dependencies
```bash
npm install
```

### 3) Add environment variables
Create `.env` in the project root and fill in the `VITE_FIREBASE_*` and `VITE_GOOGLE_MAPS_API_KEY` values from the [Environment Variables](#-environment-variables) section above.

### 4) Start development server
```bash
npm run dev
```

Then open the local URL shown by Vite (commonly `http://localhost:5173`).

---

## 📜 Available Scripts

```bash
npm run dev      # start dev server
npm run build    # production build
npm run lint     # lint project
npm run preview  # preview production build
```

---

## 🧾 Data Model (Firestore)

### `users`
- `email`
- `displayName`
- `role` (`donor` | `ngo`)
- `createdAt`

### `donations`
- `donorId`, `donorName`
- `title`, `description`, `quantity`, `foodType`
- `expiryTime`, `pickupWindow`
- `location` (`lat`, `lng`, `address`)
- `status` (`available` | `claimed` | `picked` | `expired`)
- optional claim metadata: `claimedBy`, `claimedByName`, `claimedAt`
- `createdAt`

---

## 📝 Notes

- Some UI labels still contain older naming in a few places (e.g., "ZeroWaste DineMap" text), but app functionality is wired to Left2Lift flows.
- Firestore indexes may be required for combined `where + orderBy` queries used in dashboards.

---

## 📄 License

This project is licensed under the MIT License.
