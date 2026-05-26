# 🔒 Security & Environment Setup Guide

## ⚠️ IMPORTANT: Your Credentials May Already Be Public!

If you already pushed your code to GitHub with `.env` file before adding it to `.gitignore`, your **MongoDB credentials are exposed**!

---

## 🚨 If Credentials Are Exposed

### Step 1: Change MongoDB Password Immediately
1. Go to **MongoDB Atlas**: https://www.mongodb.com/cloud/atlas
2. **Security** → **Database Access**
3. **Edit** your database user
4. **Change the password** to something new
5. Update `.env` with the new password

### Step 2: Remove `.env` From Git History
```bash
# Remove .env from git history (only if pushed)
git rm --cached .env
git commit -m "Remove .env from version control"
git push
```

### Step 3: Keep Only `.env.example`
Only `.env.example` should be in git (no real credentials)

---

## ✅ Environment Files Setup

### Backend Setup
1. Copy `.env.example` to `.env`:
   ```bash
   cp backend/.env.example backend/.env
   ```

2. Edit `backend/.env` with **your real credentials**:
   ```env
   PORT=5000
   JWT_SECRET=change_me_to_a_strong_secret_key
   NODE_ENV=development
   MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/quiz-app
   ```

### Frontend Setup
1. Copy `.env.example` to `.env.local`:
   ```bash
   cp Quiz-App-/.env.example Quiz-App-/.env.local
   ```

2. Edit `Quiz-App-/.env.local`:
   ```env
   VITE_API_URL=http://localhost:5000
   ```

---

## 📋 Files That Should NEVER Be Committed

These files are now protected by `.gitignore`:
- ✅ `.env` - Contains sensitive credentials (MongoDB password, JWT secret)
- ✅ `node_modules/` - Automatically ignored
- ✅ `.DS_Store` - OS files
- ✅ Build artifacts

---

## ✅ What SHOULD Be Committed

- ✅ `.env.example` - Template for developers
- ✅ `.gitignore` - Rules to protect sensitive files
- ✅ Source code (`.js`, `.jsx`, `.json`)
- ✅ `README.md` - Setup instructions

---

## 🔍 Verify Your Setup

### Check backend `.gitignore`:
```bash
cat backend/.gitignore | grep -E "\.env|\.local"
```

Expected output:
```
.env
.env.local
.env.*.local
```

### Check if `.env` is tracked:
```bash
git ls-files | grep .env
```

Expected: **No output** (means .env is not tracked) ✅

---

## 🚀 Production Security Tips

1. **Never hardcode secrets** in code
2. **Use environment variables** for all credentials
3. **Rotate MongoDB password** every month
4. **Use strong JWT_SECRET** (at least 32 characters)
5. **Use .env files only locally**, not in production
6. **Use environment services** like:
   - Heroku Config Vars
   - AWS Secrets Manager
   - Azure Key Vault
   - Digital Ocean App Platform

---

## 📚 Example JWT_SECRET Formats

**Weak (❌ Don't use):**
```
JWT_SECRET=secret123
```

**Strong (✅ Use this):**
```
JWT_SECRET=a7f9k2m8x1q3w5e7r2t4u9i0p5l3k9j2x7c6v5b4n8m9q2w5e7r
```

Generate strong secret:
```bash
node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"
```

---

## ✅ Final Checklist

- [ ] Updated both `.gitignore` files
- [ ] Created `.env.example` files
- [ ] Changed MongoDB password
- [ ] Updated `.env` with new credentials
- [ ] Verified `.env` is not in git with `git ls-files | grep .env`
- [ ] Committed and pushed changes

---

## 🆘 Need Help?

**Check git status:**
```bash
git status
```

**View what will be committed:**
```bash
git diff --cached
```

**Remove accidentally tracked file:**
```bash
git rm --cached backend/.env
```

