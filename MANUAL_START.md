# RESQ - Manual Startup Guide

## Quick Start Instructions

### Step 1: Create Database (One-Time Setup)

Open PostgreSQL (pgAdmin or command line) and run:

```sql
CREATE DATABASE resq_db;
```

### Step 2: Start Backend Server

Open a PowerShell terminal in the project directory and run:

```powershell
# Activate virtual environment
.\venv\Scripts\activate

# Navigate to backend
cd backend

# Start server
uvicorn app.main:socket_app --reload --host 0.0.0.0 --port 8000
```

**Keep this terminal open!** Backend will run on http://localhost:8000

### Step 3: Start Frontend Server

Open a **NEW** PowerShell terminal in the project directory and run:

```powershell
# Navigate to frontend
cd frontend

# Start development server
npm run dev
```

**Keep this terminal open!** Frontend will run on http://localhost:3000

### Step 4: Access the Application

Open your browser and go to: **http://localhost:3000**

### Default Login Credentials

**Admin:**
- Email: `admin@resq.net`
- Password: `admin123`

**To test as Citizen:**
1. Click "Citizen" card
2. Register with any phone number
3. Create password and login

**To test as Volunteer:**
1. Click "Volunteer" card  
2. Register with a Volunteer ID (e.g., `VOL001`)
3. Create password and login

---

## Troubleshooting

### Backend won't start
- Make sure PostgreSQL is running
- Verify database `resq_db` exists
- Check that virtual environment is activated (you should see `(venv)` in terminal)
- Ensure you're in the `backend` directory

### Frontend won't start
- Make sure you're in the `frontend` directory
- If you see errors, try: `npm install` first
- Check that backend is running on port 8000

### Can't connect to the application
- Verify both terminals are still running
- Backend should show: "Application startup complete"
- Frontend should show: "Ready in X seconds"

---

## API Documentation

While servers are running, you can explore the API at:
- **Swagger UI**: http://localhost:8000/docs
- **ReDoc**: http://localhost:8000/redoc

---

## Stopping the Servers

Press `Ctrl+C` in each terminal window to stop the servers.

---

## Features to Test

1. **Citizen Dashboard**
   - Send SOS emergency request
   - Report an incident with details
   - View your requests

2. **Volunteer Dashboard**
   - Toggle online/offline status
   - View assigned tasks
   - Update task status

3. **Admin Dashboard**
   - View all SOS requests and incidents
   - Assign tasks to volunteers
   - Manage users
   - Send broadcasts

All updates happen in **real-time** - no page refresh needed!
