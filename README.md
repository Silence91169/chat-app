# 💬 MyChatApp — Real-time Chat Application

![Status](https://img.shields.io/badge/status-active-brightgreen)
![Frontend](https://img.shields.io/badge/frontend-React_19-61DAFB?logo=react)
![Backend](https://img.shields.io/badge/backend-Express.js_5-000000?logo=express)
![Database](https://img.shields.io/badge/database-MongoDB-47A248?logo=mongodb)
![Real-time](https://img.shields.io/badge/realtime-Socket.io-010101?logo=socketdotio)
![Auth](https://img.shields.io/badge/auth-JWT-orange)
![Build](https://img.shields.io/badge/build-Vite_7-646CFF?logo=vite)
![Styling](https://img.shields.io/badge/styling-Tailwind_CSS-38B2AC?logo=tailwindcss)
![Cloud](https://img.shields.io/badge/cloud-Cloudinary-3448C5?logo=cloudinary)
![Email](https://img.shields.io/badge/email-Brevo-0B996E)
![Deploy](https://img.shields.io/badge/deploy-Vercel_+_Render-000000?logo=vercel)
![License](https://img.shields.io/badge/license-ISC-blue)

MyChatApp is a modern, full-stack real-time chat application that brings people together through seamless instant messaging. Built with React and Express.js, it features real-time communication powered by Socket.io, a comprehensive friend management system, and a beautiful, responsive UI. Users can register with OTP email verification, manage their profiles with custom avatars, discover other users globally, send friend requests, and engage in private conversations with real-time typing indicators and online status tracking. Whether you're connecting with friends or meeting new people, MyChatApp delivers a smooth, secure, and engaging chat experience.

## Table of Contents

- [💬 MyChatApp — Real-time Chat Application](#-mychatapp--real-time-chat-application)
  - [Table of Contents](#table-of-contents)
  - [📌 Live Services](#-live-services)
  - [📁 Repository Structure](#-repository-structure)
  - [🛠 Tech Stack](#-tech-stack)
    - [Languages \& Frameworks](#languages--frameworks)
    - [Libraries \& Tools](#libraries--tools)
  - [🧩 High-Level Architecture](#-high-level-architecture)
  - [🚀 Features](#-features)
    - [Authentication \& Security](#authentication--security)
    - [User Management](#user-management)
    - [Friend System](#friend-system)
    - [Messaging](#messaging)
    - [Chat Experience](#chat-experience)
    - [UI/UX](#uiux)
  - [📡 API Endpoints](#-api-endpoints)
    - [Authentication Routes](#authentication-routes)
    - [User Routes](#user-routes)
    - [Friend Routes](#friend-routes)
    - [Message Routes](#message-routes)
    - [Room Routes](#room-routes)
    - [Profile Routes](#profile-routes)
  - [⚙️ Installation (Local Development)](#️-installation-local-development)
    - [Prerequisites](#prerequisites)
    - [1) Clone the repository](#1-clone-the-repository)
    - [2) Backend Setup](#2-backend-setup)
    - [3) Frontend Setup](#3-frontend-setup)
  - [🔐 Environment Variables](#-environment-variables)
    - [Backend (`backend/.env`)](#backend-backendenv)
    - [Frontend (`frontend/.env`)](#frontend-frontendenv)
  - [🧪 Usage Guide](#-usage-guide)
    - [Running the Application](#running-the-application)
    - [Available Scripts](#available-scripts)
  - [🗺️ Roadmap](#️-roadmap)
    - [Planned Features](#planned-features)
    - [Known Issues](#known-issues)
  - [👥 Authors](#-authors)

<a id="live-services"></a>

## 📌 Live Services

| Layer  | Platform | Link                                           |
| ------ | -------- | ---------------------------------------------- |
| Web    | Vercel   | https://chat-app-client-gules.vercel.app       |
| Server | Render   | https://chat-app-api-59jt.onrender.com         |

<a id="repository-structure"></a>

## 📁 Repository Structure

```
chat-app/
├─ backend/                          # Backend: Express + MongoDB + Socket.io
│  ├─ server.js                      # Main server entry point
│  ├─ package.json                   # Backend dependencies
│  ├─ admin/                         # Admin utilities
│  │  ├─ deleteAllMessages.js        # Script to delete all messages
│  │  └─ resetDatabase.js            # Script to reset the database
│  ├─ config/
│  │  ├─ cloudinary.js               # Cloudinary configuration for image uploads
│  │  └─ db.js                       # MongoDB connection setup
│  ├─ controllers/
│  │  ├─ auth.controller.js          # Login, logout, token refresh
│  │  ├─ authOtp.controller.js       # OTP-based signup flow
│  │  ├─ friend.controller.js        # Friend request management
│  │  ├─ messages.controller.js      # Message CRUD operations
│  │  ├─ profile.controller.js       # Profile updates and avatar
│  │  ├─ room.controller.js          # Chat room management
│  │  └─ users.controller.js         # User discovery
│  ├─ middleware/
│  │  ├─ authenticate.js             # JWT authentication middleware
│  │  └─ multer.js                   # File upload middleware
│  ├─ model/
│  │  ├─ friend.model.js             # Friendship schema
│  │  ├─ messages.model.js           # Message schema
│  │  ├─ rooms.model.js              # Chat room schema
│  │  ├─ signupOtp.model.js          # OTP verification schema
│  │  └─ user.model.js               # User schema
│  ├─ routes/
│  │  ├─ auth.routes.js              # /api/auth routes
│  │  ├─ friend.routes.js            # /api/friends routes
│  │  ├─ messages.routes.js          # /api/messages routes
│  │  ├─ profile.routes.js           # /api/profile routes
│  │  ├─ room.routes.js              # /api/rooms routes
│  │  └─ users.routes.js             # /api/users routes
│  ├─ socket/
│  │  ├─ index.js                    # Socket.io initialization
│  │  ├─ chat.js                     # Real-time chat handlers
│  │  ├─ friend.js                   # Real-time friend request handlers
│  │  ├─ userStatus.js               # Online/offline status tracking
│  │  └─ middleware/
│  │     └─ auth.js                  # Socket authentication middleware
│  ├─ uploads/                       # Temporary file uploads
│  └─ utils/
│     ├─ createOrGetRoom.js          # Room utility functions
│     ├─ sendEmail.js                # Brevo email service for OTP
│     └─ uploadImage.js              # Cloudinary upload utility
│
└─ frontend/                         # Frontend: React + Vite + Tailwind CSS
   ├─ index.html                     # HTML entry point
   ├─ package.json                   # Frontend dependencies
   ├─ vite.config.js                 # Vite configuration
   ├─ vercel.json                    # Vercel deployment config
   └─ src/
      ├─ main.jsx                    # React entry point
      ├─ App.jsx                     # App router and routes
      ├─ App.css                     # Global styles
      ├─ index.css                   # Tailwind imports
      ├─ api/
      │  └─ axios.jsx                # Axios instance with interceptors
      ├─ assets/                     # Static assets
      ├─ components/
      │  ├─ ChatSection.jsx          # Main chat interface
      │  ├─ ChatSidebar.jsx          # Navigation sidebar
      │  ├─ FriendsSection.jsx       # Friend management UI
      │  ├─ GlobalSection.jsx        # User discovery page
      │  ├─ ProfileSettings.jsx      # Profile settings page
      │  └─ VerifyOtp.jsx            # OTP verification component
      ├─ pages/
      │  ├─ Home.jsx                 # Main dashboard
      │  ├─ Login.jsx                # Login page
      │  └─ Signup.jsx               # Signup page
      ├─ socket/
      │  └─ index.js                 # Socket.io client setup
      └─ utils/
         └─ ProtectedRoute.jsx       # Auth route protection
```

<a id="tech-stack"></a>

## 🛠 Tech Stack

### Languages & Frameworks

- **Frontend:** React 19, JavaScript (ES Modules)
- **Backend:** Express.js 5, Node.js
- **Database:** MongoDB with Mongoose ODM
- **Real-time:** Socket.io

### Libraries & Tools

- **UI:** Tailwind CSS, Lucide Icons
- **Notifications:** React Hot Toast
- **Routing:** React Router DOM v7
- **HTTP Client:** Axios
- **Authentication:** JSON Web Tokens (JWT), bcryptjs
- **File Uploads:** Multer, Cloudinary
- **Email Service:** Brevo (Sendinblue) for OTP emails
- **Build Tool:** Vite 7
- **Development:** Nodemon, ESLint
- **Deployment:** Vercel (frontend), Render (backend)

<a id="high-level-architecture"></a>

## 🧩 High-Level Architecture

```
   ┌──────────────────────┐        ┌─────────────────────────┐        ┌─────────────────┐
   │   React + Vite       │  HTTP  │   Express.js API        │ Mongoose│   MongoDB       │
   │   (Frontend)         ├───────>│   /api/auth             ├────────>│   (Users,       │
   │                      │        │   /api/users            │         │    Messages,    │
   │   Tailwind CSS       │ Socket │   /api/friends          │         │    Rooms,       │
   │   React Router       ├───────>│   /api/messages         │         │    Friendships) │
   └──────────────────────┘  .io   │   /api/rooms            │         └─────────────────┘
                                   │   /api/profile          │
                                   └─────────────────────────┘
                                             │
                       ┌─────────────────────┼─────────────────────┐
                       │                     │                     │
                       ▼                     ▼                     ▼
              ┌────────────────┐   ┌────────────────┐   ┌────────────────┐
              │   Cloudinary   │   │     Brevo      │   │   Socket.io    │
              │   (Avatars)    │   │   (OTP Email)  │   │   (Real-time)  │
              └────────────────┘   └────────────────┘   └────────────────┘
```

**Key Architecture Details:**

- **Authentication:** JWT-based with access tokens (1 hour) and refresh tokens (7 days) stored in httpOnly cookies
- **Real-time Communication:** Socket.io handles live messaging, online status, and friend request notifications
- **Token Refresh:** Automatic token rotation with failed request retry queue
- **File Storage:** Avatar images uploaded to Cloudinary via Multer middleware
- **Email Verification:** OTP-based signup flow using Brevo SMTP API
- **CORS:** Configured for frontend origin with credentials enabled

<a id="features"></a>

## 🚀 Features

### Authentication & Security
- Email + password registration with OTP verification
- Secure login with JWT access and refresh tokens
- Automatic token refresh with request retry mechanism
- Password hashing with bcryptjs
- Protected routes for authenticated users only

### User Management
- Custom user profiles with avatar uploads
- Profile name and password updates
- Global user discovery with pagination
- Real-time online/offline status tracking
- Last seen timestamps for offline users

### Friend System
- Send, accept, and reject friend requests
- Cancel outgoing friend requests
- Remove existing friends
- View pending, sent, accepted, and rejected requests
- Real-time friend request notifications

### Messaging
- Private one-on-one chat rooms
- Real-time message delivery via Socket.io
- Unsend messages functionality
- Unread message count tracking
- Mark messages as read
- Message history persistence

### Chat Experience
- Search and filter conversations
- Sort chats alphabetically or by recent activity
- Filter to show unread chats only
- Online status indicators
- Responsive chat interface
- Toast notifications for actions

### UI/UX
- Modern, clean design with Tailwind CSS
- Responsive layout for all screen sizes
- Gradient accents and smooth transitions
- Loading states and error handling
- Navigation sidebar with tab switching

<a id="api-endpoints"></a>

## 📡 API Endpoints

Base URL (local): `http://localhost:5000`  
All authenticated routes require a valid Bearer token in the Authorization header.

### Authentication Routes

| Endpoint              | Method | Description                              | Access  |
| --------------------- | ------ | ---------------------------------------- | ------- |
| `/api/auth/send-otp`  | POST   | Send OTP to email for signup             | Public  |
| `/api/auth/verify-otp`| POST   | Verify OTP and create account            | Public  |
| `/api/auth/login`     | POST   | Login with email and password            | Public  |
| `/api/auth/refresh-token` | POST | Refresh access token using cookie    | Public  |
| `/api/auth/logout`    | POST   | Logout and clear refresh token           | Public  |

### User Routes

| Endpoint           | Method | Description                              | Access        |
| ------------------ | ------ | ---------------------------------------- | ------------- |
| `/api/users/all`   | GET    | Get all users with pagination            | Auth required |

### Friend Routes

| Endpoint                       | Method | Description                    | Access        |
| ------------------------------ | ------ | ------------------------------ | ------------- |
| `/api/friends/request`         | POST   | Send a friend request          | Auth required |
| `/api/friends/accept`          | POST   | Accept a friend request        | Auth required |
| `/api/friends/reject`          | POST   | Reject a friend request        | Auth required |
| `/api/friends/remove`          | POST   | Remove an existing friend      | Auth required |
| `/api/friends/cancel`          | POST   | Cancel a sent friend request   | Auth required |
| `/api/friends/pending`         | GET    | Get pending friend requests    | Auth required |
| `/api/friends/sent`            | GET    | Get sent friend requests       | Auth required |
| `/api/friends/list`            | GET    | Get accepted friends list      | Auth required |
| `/api/friends/rejected`        | GET    | Get rejected requests          | Auth required |
| `/api/friends/status/:friendId`| GET    | Check friendship status        | Auth required |

### Message Routes

| Endpoint                       | Method | Description                    | Access        |
| ------------------------------ | ------ | ------------------------------ | ------------- |
| `/api/messages/:roomId`        | GET    | Get messages for a room        | Auth required |
| `/api/messages`                | POST   | Send a message                 | Auth required |
| `/api/messages/unsend/:messageId` | PUT | Unsend a message              | Auth required |

### Room Routes

| Endpoint                       | Method | Description                    | Access        |
| ------------------------------ | ------ | ------------------------------ | ------------- |
| `/api/rooms/my`                | GET    | Get user's chat rooms          | Auth required |
| `/api/rooms/with/:friendId`    | GET    | Get or create room with friend | Auth required |
| `/api/rooms/:roomId/mark-read` | POST   | Mark room messages as read     | Auth required |

### Profile Routes

| Endpoint                  | Method | Description                    | Access        |
| ------------------------- | ------ | ------------------------------ | ------------- |
| `/api/profile/update`     | PUT    | Update profile name            | Auth required |
| `/api/profile/avatar`     | PUT    | Upload/update avatar image     | Auth required |
| `/api/profile/change-password` | PUT | Change account password       | Auth required |

<a id="installation-local-development"></a>

## ⚙️ Installation (Local Development)

<a id="prerequisites"></a>

### Prerequisites

- **Node.js** >= 18.x
- **npm** or **yarn**
- **MongoDB** (local or MongoDB Atlas)
- **Cloudinary** account (for avatar uploads)
- **Brevo** account (for OTP emails)

<a id="1-clone-the-repository"></a>

### 1) Clone the repository

```bash
git clone https://github.com/silence91169/chat-app.git
cd chat-app
```

<a id="2-backend-setup"></a>

### 2) Backend Setup

```bash
cd backend
npm install
```

Create a `.env` file in the `backend` directory (see [Environment Variables](#-environment-variables)).

Start the backend server:

```bash
# Development mode with hot reload
npm run dev

# Production mode
npm start
```

The backend will run on `http://localhost:5000`.

<a id="3-frontend-setup"></a>

### 3) Frontend Setup

```bash
cd frontend
npm install
```

Create a `.env` file in the `frontend` directory (see [Environment Variables](#-environment-variables)).

Start the frontend development server:

```bash
npm run dev
```

The frontend will run on `http://localhost:5173`.

<a id="environment-variables"></a>

## 🔐 Environment Variables

### Backend (`backend/.env`)

```env
# Server
PORT=5000
NODE_ENV=development

# MongoDB Connection
MONGO_URI=mongodb://localhost:27017/chatapp

# JWT Secrets (use strong random strings)
ACCESS_TOKEN_SECRET=your-access-token-secret
REFRESH_TOKEN_SECRET=your-refresh-token-secret

# Frontend URL (for CORS)
FRONTEND_URL=http://localhost:5173

# Cloudinary Configuration
CLOUDINARY_CLOUD_NAME=your-cloud-name
CLOUDINARY_API_KEY=your-api-key
CLOUDINARY_API_SECRET=your-api-secret

# Brevo Email Configuration
BREVO_API_KEY=your-brevo-api-key
EMAIL=your-verified-sender-email@example.com
```

### Frontend (`frontend/.env`)

```env
# Backend API URL
VITE_API_URL=http://localhost:5000
```

<a id="usage-guide"></a>

## 🧪 Usage Guide

### Running the Application

1. Start the backend server (from `backend/` directory):
   ```bash
   npm run dev
   ```

### Frontend Testing
```bash
cd frontend
npm test
```

---

## 🚀 Deployment

### Backend Deployment (Railway/Render/Heroku)

1. Set environment variables in your hosting platform
2. Update `FRONTEND_URL` to your production URL
3. Set `NODE_ENV=production`
4. Deploy using Git or CLI

### Frontend Deployment (Vercel/Netlify)

1. Build the project:
```bash
npm run build
```

2. Set `VITE_API_URL` to your backend URL
3. Deploy the `dist` folder

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👨‍💻 Author

**Aryan Kinha**
- GitHub: [@aryankinha](https://github.com/Silence91169)
- Repository: [chattingAPP](https://github.com/Silence91169/chat-app)

---

## 🙏 Acknowledgments

- [React](https://react.dev/) - Frontend framework
- [Express](https://expressjs.com/) - Backend framework
- [MongoDB](https://www.mongodb.com/) - Database
- [Socket.IO](https://socket.io/) - Real-time engine
- [Tailwind CSS](https://tailwindcss.com/) - Styling
- [Cloudinary](https://cloudinary.com/) - Image hosting
- [Brevo](https://www.brevo.com/) - Email service

---

## 📞 Support

If you have any questions or need help, please:
- Open an [issue](https://github.com/aryankinha/chattingAPP/issues)
- Contact: [your-email@example.com](mailto:your-email@example.com)

---

<div align="center">

Made with ❤️ by Aryan Kinha

⭐ Star this repository if you found it helpful!

</div>
