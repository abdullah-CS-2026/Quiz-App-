# MongoDB Setup Guide for Quiz App

## Step 1: Create MongoDB Atlas Account & Cluster

1. **Go to MongoDB Atlas**: https://www.mongodb.com/cloud/atlas
2. **Sign up** (free account)
3. **Create a new project** (name: Quiz-App)
4. **Build a database** → Choose **Free tier (M0)**
5. **Select region** (choose closest to you)
6. **Wait for cluster** to be created (2-3 minutes)

---

## Step 2: Get MongoDB Connection String

1. In MongoDB Atlas, click **"Databases"**
2. Click **"Connect"** on your cluster
3. Choose **"Drivers"** → Select **"Node.js"**
4. Copy the connection string
   - It looks like: `mongodb+srv://username:password@cluster0.xxxxx.mongodb.net/?retryWrites=true&w=majority`

---

## Step 3: Update `.env` File

1. Open `backend/.env`
2. Replace the MONGODB_URI with your connection string:

```env
PORT=5000
JWT_SECRET=your_super_secret_jwt_key_change_this_in_production
NODE_ENV=development
MONGODB_URI=mongodb+srv://your_username:your_password@cluster0.xxxxx.mongodb.net/quiz-app?retryWrites=true&w=majority
```

**⚠️ IMPORTANT:**
- Replace `your_username` and `your_password` with the database user credentials you created
- Keep the `/quiz-app` at the end (this is your database name)
- Do NOT include `<>` brackets

---

## Step 4: Create Database User (Security)

If MongoDB Atlas asks for credentials:

1. In MongoDB Atlas → **Security** → **Database Access**
2. Click **"Add New Database User"**
3. Choose **"Password"** authentication
4. Enter username & password
5. Click **"Add User"**
6. Use these credentials in your connection string

---

## Step 5: Test Backend Connection

1. Open terminal and navigate to backend:
   ```bash
   cd backend
   npm run dev
   ```

2. You should see:
   ```
   ✅ MongoDB connected successfully
   🚀 Server is running on http://localhost:5000
   ```

If you see ❌ connection error:
- Check if your connection string is correct in `.env`
- Make sure IP is whitelisted (MongoDB Atlas → Network Access → Allow from anywhere for testing)

---

## Step 6: Download MongoDB Compass (GUI)

1. Download: https://www.mongodb.com/products/compass
2. Install it
3. Open MongoDB Compass
4. Click **"New Connection"**
5. Paste your connection string
6. Click **"Connect"**

---

## Step 7: View Your Data in Compass

1. In MongoDB Compass, expand your cluster
2. Click on **"quiz-app"** database
3. You'll see a **"users"** collection
4. Click on **"users"** to view all registered users

Each user entry will show:
```json
{
  "_id": "507f1f77bcf86cd799439011",
  "name": "John Doe",
  "email": "john@example.com",
  "passwordHash": "hashed_password_here",
  "createdAt": "2025-05-25T10:30:00.000Z"
}
```

---

## Full Setup Workflow

### Terminal 1 - Backend:
```bash
cd backend
npm run dev
```
Expected output:
```
✅ MongoDB connected successfully
🚀 Server is running on http://localhost:5000
```

### Terminal 2 - Frontend:
```bash
cd Quiz-App-
npm run dev
```
Expected output:
```
  VITE v6.3.4  ready in 123 ms

  ➜  Local:   http://localhost:5173/
```

---

## Testing the Flow

1. Open http://localhost:5173
2. Click **"Sign up here"**
3. Create an account
4. Open **MongoDB Compass**
5. Your user should appear in the `users` collection automatically ✅

---

## Database Structure

### Users Collection

```javascript
{
  "_id": ObjectId,           // MongoDB's unique ID
  "name": String,            // User's full name
  "email": String,           // User's email (unique)
  "passwordHash": String,    // Encrypted password
  "createdAt": Date          // Account creation timestamp
}
```

---

## Common Issues & Solutions

### Error: `connect ECONNREFUSED`
- MongoDB URI is wrong
- Check `.env` file for correct connection string

### Error: `authentication failed`
- Username/password is incorrect
- Check if database user exists in MongoDB Atlas

### Error: `no suitable servers found`
- Your IP is not whitelisted
- MongoDB Atlas → Network Access → Allow 0.0.0.0/0 (for testing)

### Error: `User already exists`
- This is normal - means email is already registered

---

## Useful MongoDB Compass Tips

- **Search users**: Click filter icon, enter `{ "email": "user@example.com" }`
- **Delete user**: Right-click user → Delete
- **Edit user**: Click on document → Edit
- **Export data**: Right-click collection → Export

---

## Next Steps (Optional)

- Add email verification
- Add password reset
- Add quiz scores storage
- Create admin dashboard

