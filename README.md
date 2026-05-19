<div align="center">
<img src="https://img.shields.io/badge/Left2Lift-Food%20Redistribution%20Platform-22c55e?style=for-the-badge&logo=leaf&logoColor=white" alt="Left2Lift" />
<br/>
<br/>
Connecting food donors with NGOs to eliminate food waste and power last-mile food redistribution.
<br/>
<!-- Tech Stack Badges -->
Show Image
Show Image
Show Image
Show Image
Show Image
Show Image
Show Image
<br/>
Show Image
Show Image
Show Image
</div>

📖 Table of Contents

Overview
How It Works
Features
Tech Stack
Project Structure
Getting Started
Environment Variables
Available Scripts
Data Model
Notes
License


🌍 Overview
Left2Lift is a role-based web application that bridges the gap between surplus food and people who need it most.
RoleWhat they do🍽️ DonorsRestaurants and event organizers post surplus food pickups🤝 NGOsDiscover nearby donations, claim them, and navigate to pickup locations
The platform provides real-time updates, map-based discovery, and route optimization — making food redistribution fast, transparent, and efficient.

🔄 How It Works
Donor posts surplus food
        │
        ▼
Donation stored in Firestore (status: available)
        │
        ▼
NGO sees real-time donation feed on their dashboard
        │
        ▼
NGO claims a donation (status: claimed)
        │
        ▼
NGO navigates using in-app map route tools
        │
        ▼
Pickup completed and tracked (status: picked)

✨ Features
🔐 Authentication & Roles

Email/password sign-up and login via Firebase Authentication
Role selection at signup: Donor or NGO
Role-based routing — /donor and /ngo dashboards


🍽️ Donor Features

Post donations with full details:

Title, description, quantity, and food type
Best-before datetime and pickup window
Address + GPS coordinates


Google Places Autocomplete for address input
Browser geolocation auto-fill as fallback
Dashboard with live donation status cards:

Total · Available · Claimed · Completed




🤝 NGO Features

Real-time donation feed from Firestore
Toggle between Map View and List View
Smart filters: All Available · Available Now · Claimed · Mine
Claim donation flow with Firestore status sync
Quick-open in Google Maps (directions fallback to search)
Live map markers with popup info windows
Multi-pickup route planner:

Waypoint optimization via Google Directions API
ETA + distance display
Progress tracking and completion flow


In-app push notifications for new donations


🎨 UI / UX

Fully responsive dashboards for both roles
Status-aware donation cards with visual badges
Modal-based posting and route flows
Clean, accessible design powered by Tailwind CSS


🛠️ Tech Stack
LayerTechnologyFrontend FrameworkShow Image React 18 + TypeScriptBuild ToolShow Image Vite 5RoutingShow Image React Router DOM 7StylingShow Image Tailwind CSSIconsShow Image Lucide ReactAuthShow Image Firebase AuthenticationDatabaseShow Image Cloud FirestoreStorageShow Image Firebase StorageMapsShow Image Maps · Places · Geometry · Directions

📂 Project Structure
Left2Lift/
├── public/
├── src/
│   ├── components/
│   │   ├── Auth/           # Login, Signup, Role selection
│   │   ├── Donor/          # Donor dashboard & post-donation forms
│   │   ├── NGO/            # NGO feed, map view, route planner
│   │   └── Layout/         # Shared layout wrappers, navbar
│   ├── config/
│   │   └── firebase.ts     # Firebase app initialization
│   ├── hooks/
│   │   ├── useAuth.ts      # Auth state & role management
│   │   └── useGoogleMaps.ts # Maps API loader & helpers
│   ├── types/
│   │   └── index.ts        # Shared TypeScript interfaces
│   └── App.tsx             # Root component & route definitions
├── .env                    # Environment variables (not committed)
├── .env.example            # Template for environment setup
├── index.html
├── package.json
├── tailwind.config.ts
├── tsconfig.json
└── vite.config.ts

🚀 Getting Started
Prerequisites
Make sure you have these installed:

Show Image Node.js v18 or higher
Show Image npm v9+ (or yarn/pnpm)
A Firebase project — create one here
A Google Cloud project with Maps APIs enabled — console here


Step-by-step Setup
1. Clone the repository
bashgit clone https://github.com/Tejas164321/Left2Lift.git
cd Left2Lift
2. Install dependencies
bashnpm install
3. Configure environment variables
bashcp .env.example .env
# Then open .env and fill in your keys (see Environment Variables section below)
4. Start the development server
bashnpm run dev
Open your browser at http://localhost:5173 🎉

🔐 Environment Variables
Create a .env file in the project root with the following keys:
env# ── Firebase Configuration ────────────────────────────────────────
VITE_FIREBASE_API_KEY=your_firebase_api_key
VITE_FIREBASE_AUTH_DOMAIN=your-project-id.firebaseapp.com
VITE_FIREBASE_PROJECT_ID=your-project-id
VITE_FIREBASE_STORAGE_BUCKET=your-project-id.appspot.com
VITE_FIREBASE_MESSAGING_SENDER_ID=your_sender_id
VITE_FIREBASE_APP_ID=your_app_id

# ── Google Maps ───────────────────────────────────────────────────
VITE_GOOGLE_MAPS_API_KEY=your_google_maps_api_key
🔑 Where to find these values
KeyWhere to find itVITE_FIREBASE_*Firebase Console → Project Settings → Your Apps → Web App SDK ConfigVITE_GOOGLE_MAPS_API_KEYGoogle Cloud Console → APIs & Services → Credentials → Create API Key
✅ Required Google Maps APIs
Enable these APIs in your Google Cloud project:

☑️ Maps JavaScript API
☑️ Places API
☑️ Directions API
☑️ Geometry Library (loaded via Maps JS API)


💡 Tip: Restrict your API key by HTTP referrer in production to prevent unauthorized usage.


📜 Available Scripts
bashnpm run dev       # Start development server (hot reload)
npm run build     # Production build → dist/
npm run preview   # Preview the production build locally
npm run lint      # Run ESLint across the project

🧾 Data Model (Firestore)
users collection
FieldTypeDescriptionemailstringUser email addressdisplayNamestringDisplay namerole"donor" | "ngo"User rolecreatedAttimestampAccount creation time

donations collection
FieldTypeDescriptiondonorIdstringUID of the posting donordonorNamestringDisplay name of the donortitlestringDonation titledescriptionstringDescription of the foodquantitystringAmount / portions availablefoodTypestringCategory (e.g. cooked, packaged)expiryTimetimestampBest-before datetimepickupWindowstringAvailable pickup time rangelocation.latnumberLatitudelocation.lngnumberLongitudelocation.addressstringHuman-readable addressstatus"available" | "claimed" | "picked" | "expired"Current donation statusclaimedBystring?NGO UID (when claimed)claimedByNamestring?NGO display name (when claimed)claimedAttimestamp?When the donation was claimedcreatedAttimestampWhen the donation was posted

⚠️ Firestore Indexes: Combined where + orderBy queries used in the dashboards may require composite indexes. Firestore will surface a direct link to create them in your browser console if missing.


📝 Notes

A few UI labels may still reference older naming (e.g. "ZeroWaste DineMap" text in some places) — these are cosmetic leftovers and do not affect core functionality.
Firestore Security Rules should be configured before deploying to production to restrict read/write access by role.
The Google Maps key should be HTTP-referrer restricted in production.


🤝 Contributing
Contributions, issues, and feature requests are welcome!

Fork the repo
Create a feature branch: git checkout -b feature/your-feature-name
Commit your changes: git commit -m 'feat: add your feature'
Push to the branch: git push origin feature/your-feature-name
Open a Pull Request


📄 License
This project is licensed under the MIT License — see the LICENSE file for details.

<div align="center">
Made with ❤️ to reduce food waste, one pickup at a time.
⭐ Star this repo if you find it useful!
</div>
