# RESQ - Rapid Emergency Response System

A full-stack emergency response application built with Next.js, FastAPI, PostgreSQL, and Socket.IO for real-time communication.

## Project Structure

```
resq/
├── backend/           # FastAPI backend
│   ├── app/
│   │   ├── routes/   # API endpoints
│   │   ├── models.py # Database models
│   │   ├── schemas.py# Pydantic schemas
│   │   ├── auth.py   # Authentication
│   │   └── main.py   # FastAPI app
│   ├── requirements.txt
│   └── .env
├── frontend/         # Next.js frontend
│   ├── src/
│   │   ├── app/     # Pages (App Router)
│   │   ├── lib/     # Utilities
│   │   └── store/   # State management
│   ├── package.json
│   └── .env.local
└── venv/            # Python virtual environment
```

## Features

### Core Functionality
- ✅ **Real-time Updates**: Socket.IO for instant SOS/incident notifications
- ✅ **Role-Based Access**: Citizen, Volunteer, and Admin dashboards
- ✅ **JWT Authentication**: Secure token-based auth
- ✅ **Location Tracking**: Geolocation support for emergencies
- ✅ **Task Assignment**: Admin assigns tasks to nearest volunteers
- ✅ **Chat System**: Real-time messaging and broadcasts
- ✅ **Status Management**: Volunteer online/offline status

### Citizen Features
- Report SOS emergencies
- Submit incident reports
- View assigned volunteer
- Real-time chat with responders
- View broadcast messages

### Volunteer Features
- View assigned tasks
- Accept/reject assignments
- Update task status (responding, on-site, completed)
- View nearby unassigned incidents
- Real-time notifications
- Online/offline status toggle

### Admin Features
- View all SOS requests and incidents
- Assign tasks to volunteers
- User management (CRUD operations)
- Send broadcast messages
- Real-time dashboard with statistics
- Add comments to tasks
- Complete control over the system

## Prerequisites

- **Node.js** 18+ 
- **Python** 3.9+
- **PostgreSQL** 13+

## Setup Instructions

### 1. Database Setup

Install PostgreSQL and create a database:

```sql
CREATE DATABASE resq_db;
```

### 2. Backend Setup

```bash
# Navigate to project root
cd resq

# Activate virtual environment (already created)
.\venv\Scripts\activate

# Install Python dependencies (already done)
pip install -r backend\requirements.txt

# Configure environment
# Update backend\.env with your database credentials

# Run backend server
cd backend
uvicorn app.main:socket_app --reload --host 0.0.0.0 --port 8000
```

Backend will be available at:
- API: http://localhost:8000
- Docs: http://localhost:8000/docs
- WebSocket: ws://localhost:8000/socket.io

### 3. Frontend Setup

Open a new terminal:

```bash
# Navigate to frontend
cd resq\frontend

# Install dependencies
npm install

# Run development server
npm run dev
```

Frontend will be available at http://localhost:3000

## Default Credentials

### Admin Access
- **Email**: admin@resq.net
- **Password**: admin123

### Test Users
You can register new users for Citizen and Volunteer roles from the landing page.

## Usage Guide

### For Citizens

1. Go to http://localhost:3000
2. Select "Citizen" tab
3. Register with phone number or login
4. Click "EMERGENCY SOS" for immediate help
5. Or use "Report Incident" for non-emergency reports

### For Volunteers

1. Go to http://localhost:3000
2. Select "Volunteer" tab
3. Login with volunteer ID
4. Toggle status to "ONLINE"
5. View and accept assigned tasks
6. Update task status as you progress

### For Admins

1. Go to http://localhost:3000
2. Select "Command Center" tab
3. Login with admin credentials
4. View all SOS requests and incidents
5. Assign tasks to online volunteers
6. Manage users and send broadcasts

## API Endpoints

### Authentication
- `POST /api/auth/register` - Register user
- `POST /api/auth/login` - Login user

### Users
- `GET /api/users/me` - Get profile
- `PUT /api/users/me` - Update profile
- `PUT /api/users/me/location` - Update location
- `GET /api/users/volunteers/online` - Get online volunteers

### SOS & Incidents
- `POST /api/sos/` - Create SOS (Citizen)
- `POST /api/incidents/` - Create incident (Citizen)
- `GET /api/sos/` - Get all SOS
- `GET /api/incidents/` - Get all incidents

### Tasks
- `POST /api/tasks/` - Assign task (Admin)
- `GET /api/tasks/` - Get tasks
- `PUT /api/tasks/{id}` - Update task
- `GET /api/tasks/nearby` - Get nearby tasks (Volunteer)

### Messages & Comments
- `POST /api/messages/` - Send message
- `GET /api/messages/` - Get messages
- `POST /api/comments/` - Add comment
- `GET /api/comments/task/{id}` - Get task comments

### Dashboard
- `GET /api/dashboard/stats` - Get statistics

## Real-time Events (Socket.IO)

### Client Events
- `authenticate` - Authenticate session
- `join_room` - Join room
- `send_message` - Send message

### Server Events
- `sos_created` - New SOS alert
- `incident_created` - New incident alert
- `task_assigned` - Task assigned to volunteer
- `task_updated` - Task status updated
- `broadcast_message` - Admin broadcast
- `volunteer_status_changed` - Volunteer status change

## Technology Stack

### Backend
- FastAPI - Async web framework
- SQLAlchemy 2.0 - ORM
- PostgreSQL - Database
- python-socketio - WebSocket server
- JWT - Authentication
- Uvicorn - ASGI server

### Frontend
- Next.js 14 - React framework (App Router)
- TypeScript - Type safety
- Tailwind CSS - Styling
- Socket.IO Client - Real-time communication
- Zustand - State management
- Axios - HTTP client

## Development Notes

- Virtual environment (`venv`) is already set up
- All backend dependencies are installed
- Database migrations run automatically on server start
- Frontend uses TypeScript for type safety
- Real-time updates work without page refresh
- Mobile-first responsive design

## Production Deployment

### Backend
1. Update `.env` with production database URL
2. Change `SECRET_KEY` and admin credentials
3. Set `CORS_ORIGINS` to your frontend URL
4. Use Gunicorn with Uvicorn workers:
   ```bash
   gunicorn app.main:socket_app -w 4 -k uvicorn.workers.UvicornWorker
   ```

### Frontend
1. Update `.env.local` with production API URL
2. Get a real Mapbox token for maps
3. Build and deploy:
   ```bash
   npm run build
   npm start
   ```

## Troubleshooting

### Backend Issues
- **Database connection error**: Check PostgreSQL is running and credentials in `.env`
- **Import errors**: Ensure virtual environment is activated
- **Port already in use**: Change port in uvicorn command

### Frontend Issues
- **Module not found**: Run `npm install`
- **API connection error**: Ensure backend is running on port 8000
- **Socket not connecting**: Check `NEXT_PUBLIC_SOCKET_URL` in `.env.local`

## License

MIT License - Built for interview demonstration purposes

## Contact

For questions or issues, please refer to the project documentation.
