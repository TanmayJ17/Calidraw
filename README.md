Calidraw <br>
A real-time collaborative whiteboard app inspired by Excalidraw — sketch shapes, freehand drawings, arrows and text on an infinite canvas, and see your teammates' cursors and edits update live.

<img width="1466" height="501" alt="image" src="https://github.com/user-attachments/assets/c5e20b29-a81e-4bb9-82be-2eb89ed2addc" />
<img width="894" height="497" alt="image" src="https://github.com/user-attachments/assets/bcd03932-e447-43d8-947c-b11cec423567" />

Features <br>
Freehand drawing canvas — rectangles, ellipses, lines, arrows, pencil strokes, and text tool<br>
Style customization — per-element stroke color, fill color, stroke width, and opacity controls<br>
Real-time collaboration — powered by Socket.io; every stroke and edit is broadcast instantly to everyone on the same board<br>
Live cursors — see collaborators' cursor positions on the board as they draw<br>
Persistent boards — boards and their elements are saved to MongoDB, so your work is there when you come back<br>
User authentication — JWT-based signup/login with hashed passwords (bcrypt)<br>
Multiple boards per user — create, rename, and manage your own boards from a dashboard<br>
<br>

Tech Stack<br>
<br>
Frontend<br>
React 19 + Vite<br>
React Router for navigation<br>
Zustand for state management<br>
Socket.io-client for real-time sync<br>
<br>

Backend<br>
Node.js + Express<br>
MongoDB with Mongoose<br>
Socket.io for WebSocket communication<br>
JWT (jsonwebtoken) + bcryptjs for authentication<br>
<br>

Project Structure<br>

Calidraw/<br>
├── backend/<br>
│   ├── models/          # Mongoose schemas (User, Board)<br>
│   ├── routes/          # REST endpoints (auth, boards)<br>
│   ├── middleware/       # JWT auth middleware<br>
│   ├── socket/          # Socket.io event handlers<br>
│   ├── app.js           # Express app setup<br>
│   └── server.js        # Entry point (HTTP + Socket.io + Mongo connection)<br>
└── frontend/<br>
    ├── src/<br>
    │   ├── components/  # Canvas, Toolbar, StylePanel, CursorOverlay, TopBar<br>
    │   ├── pages/        # Home, Login, Register, BoardPage<br>
    │   ├── store/        # Zustand stores (auth, board)<br>
    │   ├── hooks/        # useSocket (real-time sync logic)<br>
    │   └── utils/        # API client, drawing/hit-test/math helpers<br>
    └── vite.config.js<br>
<br>
Getting Started<br>
<br>
Prerequisites<br>
Node.js (v18+ recommended)<br>
MongoDB (local instance or a MongoDB Atlas connection string)<br>
<br>

1. Clone the repo<br>

bashgit clone https://github.com/TanmayJ17/Calidraw.git<br>
cd Calidraw<br>

2. Backend setup<br>

bashcd backend<br>
npm install<br>

Create a .env file in backend/:<br>

envPORT=3001<br>
MONGODB_URI=mongodb://localhost:27017/excalidraw<br>
JWT_SECRET=your_jwt_secret_here<br>

Run the backend:<br>

bashnpm run dev<br>

The server starts on http://localhost:3001 (health check at /api/health).<br>

3. Frontend setup<br>

bashcd frontend<br>
npm install<br>
npm run dev<br>

The app runs on https://calidraw-frontend.onrender.com<br>

<br>
How It Works<br>
<br>
Sign up / log in — the backend issues a JWT, stored client-side and sent as a Bearer token on API requests.<br>
From the dashboard, create a new board or open an existing one.<br>
Opening a board connects a Socket.io client, which joins a room keyed by the board ID.<br>
Every draw action (add/update/delete element, cursor move) is emitted over the socket and broadcast to everyone else in that room, while board state is periodically persisted to MongoDB via the REST API.<br>

<br>
Deployment<br>
Live demo: https://calidraw-frontend.onrender.com<br>
<br>
License<br>
This project is open source and available for personal and educational use.<br>
