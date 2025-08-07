# Video Conferencing App Deployment Guide

This guide will help you deploy the video conferencing application for both mobile and PC access.

## Prerequisites

1. Node.js (v14 or later)
2. npm or yarn
3. MongoDB Atlas account (for database)
4. Accounts on Vercel and Railway (or your preferred hosting services)

## Backend Deployment

### 1. Set up MongoDB Atlas

1. Go to [MongoDB Atlas](https://www.mongodb.com/cloud/atlas/register)
2. Create a free cluster
3. Create a database user and get the connection string
4. Add your IP address to the IP whitelist
5. Get the connection string (it will look like `mongodb+srv://<username>:<password>@cluster0.xxxxx.mongodb.net/`)

### 2. Deploy Backend to Railway (Recommended)

1. Sign up at [Railway.app](https://railway.app/)
2. Create a new project
3. Click "New" and select "Deploy from GitHub repo"
4. Select your repository and the `backend` directory
5. Add these environment variables:
   - `MONGODB_URI`: Your MongoDB connection string
   - `PORT`: 8000
   - `NODE_ENV`: production
   - `FRONTEND_URL`: Your frontend URL (e.g., https://your-frontend.vercel.app)
6. Deploy

### Alternative: Deploy to Render

1. Sign up at [Render.com](https://render.com/)
2. Create a new Web Service
3. Connect your GitHub repository
4. Configure:
   - Name: your-app-backend
   - Region: Choose the one closest to your users
   - Branch: main
   - Build Command: `cd backend && npm install`
   - Start Command: `cd backend && npm start`
5. Add environment variables as shown above
6. Click "Create Web Service"

## Frontend Deployment

### 1. Deploy to Vercel (Recommended)

1. Sign up at [Vercel](https://vercel.com/)
2. Import your GitHub repository
3. In project settings, configure:
   - Build Command: `npm run build`
   - Output Directory: `build`
   - Install Command: `npm install`
4. Add these environment variables:
   - `REACT_APP_API_URL`: Your deployed backend URL (e.g., https://your-backend.railway.app)
5. Deploy

### 2. Update CORS in Backend

After deploying the frontend, update the `FRONTEND_URL` in your backend environment variables to match your deployed frontend URL.

## Testing the Deployment

1. Open the frontend URL in Chrome on both mobile and PC
2. Test user registration and login
3. Test video call functionality
4. Verify that both mobile and PC can join the same meeting room

## Environment Variables

### Backend (`.env`)
```
MONGODB_URI=your_mongodb_connection_string
PORT=8000
NODE_ENV=production
FRONTEND_URL=https://your-frontend.vercel.app
```

### Frontend (Vercel/Railway environment variables)
```
REACT_APP_API_URL=https://your-backend.railway.app
```

## Troubleshooting

1. **CORS Errors**: Ensure `FRONTEND_URL` in the backend matches your deployed frontend URL exactly
2. **Database Connection**: Verify your MongoDB Atlas IP whitelist and connection string
3. **WebRTC Issues**: Ensure both clients are using HTTPS and have camera/microphone permissions
