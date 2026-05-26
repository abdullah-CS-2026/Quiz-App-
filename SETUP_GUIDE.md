# Quiz App with JWT Authentication

A full-stack Quiz application with user authentication system using JWT (JSON Web Tokens). Users must sign up and log in before they can attempt the quiz.

## Project Structure

```
Quiz_App/
├── backend/                    # Node.js/Express backend
│   ├── controllers/
│   │   └── authController.js
│   ├── middleware/
│   │   └── authMiddleware.js
│   ├── models/
│   │   └── User.js
│   ├── routes/
│   │   └── auth.js
│   ├── .env
│   ├── package.json
│   └── server.js
└── Quiz-App-/                  # React frontend
    ├── src/
    │   ├── pages/
    │   │   ├── Signup.jsx
    │   │   ├── Login.jsx
    │   │   ├── QuizPage.jsx
    │   │   └── Auth.css
    │   ├── context/
    │   │   └── AuthContext.jsx
    │   ├── Components/
    │   │   ├── ProtectedRoute.jsx
    │   │   └── Quiz/
    │   │       ├── Quiz.jsx
    │   │       └── Quiz.css
    │   ├── assets/
    │   │   └── data.js
    │   ├── App.jsx
    │   ├── App.css
    │   ├── main.jsx
    │   └── index.css
    ├── package.json
    ├── vite.config.js
    └── index.html
```

## Features

- **User Authentication**
  - Sign up with email, password, and name
  - Login with email and password
  - JWT token-based authentication
  - Secure password hashing with bcryptjs

- **Protected Routes**
  - Quiz is only accessible to authenticated users
  - Automatic redirect to login if not authenticated
  - Logout functionality

- **Quiz Features**
  - Multiple choice questions
  - Score calculation
  - Results display
  - Reset quiz functionality

## Installation & Setup

### Prerequisites
- Node.js (v14 or higher)
- npm or yarn

### Backend Setup

1. Navigate to the backend directory:
   ```bash
   cd backend
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. The `.env` file is already configured with default settings:
   ```
   PORT=5000
   JWT_SECRET=your_super_secret_jwt_key_change_this_in_production
   NODE_ENV=development
   ```

   **For production, change the `JWT_SECRET` to a strong random string.**

4. Start the backend server:
   ```bash
   npm start
   ```
   
   Or for development with auto-reload:
   ```bash
   npm run dev
   ```

   The backend will run on `http://localhost:5000`

### Frontend Setup

1. Navigate to the frontend directory:
   ```bash
   cd Quiz-App-
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Start the development server:
   ```bash
   npm run dev
   ```

   The frontend will run on `http://localhost:5173`

## Usage Flow

1. **Sign Up**
   - Open `http://localhost:5173`
   - You'll be redirected to the login page
   - Click on "Sign up here"
   - Fill in your name, email, password, and confirm password
   - Click "Sign Up"
   - You'll be redirected to the login page

2. **Login**
   - Enter your email and password
   - Click "Login"
   - You'll be redirected to the quiz page

3. **Take Quiz**
   - Answer multiple choice questions
   - Click "Next" to proceed
   - View your score at the end
   - Click "Reset" to start over
   - Use the "Logout" button in the top right to log out

## API Endpoints

### Authentication Endpoints

- **POST** `/api/auth/signup`
  - Body: `{ email, password, name, confirmPassword }`
  - Response: `{ message, user, token }`

- **POST** `/api/auth/login`
  - Body: `{ email, password }`
  - Response: `{ message, user, token }`

- **GET** `/api/auth/me`
  - Headers: `Authorization: Bearer <token>`
  - Response: `{ user }`

- **POST** `/api/auth/logout`
  - Response: `{ message }`

## Security Features

- Passwords are hashed using bcryptjs
- JWT tokens are used for stateless authentication
- Tokens expire after 24 hours
- CORS is configured to allow requests from the frontend
- Protected routes ensure only authenticated users can access the quiz

## Environment Variables

### Backend (.env)
- `PORT`: Server port (default: 5000)
- `JWT_SECRET`: Secret key for signing JWT tokens
- `NODE_ENV`: Environment (development/production)

## Technologies Used

### Backend
- Node.js
- Express.js
- JSON Web Tokens (JWT)
- bcryptjs (password hashing)
- CORS

### Frontend
- React
- React Router DOM
- Axios (HTTP client)
- Vite (build tool)

## Notes

- Currently uses in-memory user storage. For production, integrate a database like MongoDB or PostgreSQL.
- The JWT secret in `.env` is a placeholder and should be changed for production use.
- Tokens are stored in localStorage on the client side.

## Future Enhancements

- Database integration (MongoDB, PostgreSQL)
- Email verification
- Password reset functionality
- User profile management
- Quiz creation and management admin panel
- Leaderboard
- Analytics and reporting

## License

ISC
