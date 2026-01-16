# MERN Job Portal - Getting Started

## Quick Start Guide

### 1. Clone or Download the Project
```bash
cd jobfinder
```

### 2. Install Backend Dependencies
```bash
cd backend
npm install
```

### 3. Setup Backend Environment
Create `.env` file in backend directory:
```env
PORT=5000
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/jobfinder
JWT_SECRET=your_secret_key_here
NODE_ENV=development
```

### 4. Start Backend Server
```bash
npm run dev
```
Backend will run on `http://localhost:5000`

### 5. Install Frontend Dependencies (new terminal)
```bash
cd frontend
npm install
```

### 6. Setup Frontend Environment
Create `.env` file in frontend directory:
```env
REACT_APP_API_URL=http://localhost:5000/api
```

### 7. Start Frontend Server
```bash
npm start
```
Frontend will open at `http://localhost:3000`

## Testing the Application

### Create Test Accounts

**Job Seeker Account:**
- Email: `jobseeker@example.com`
- Password: `password123`
- Role: Job Seeker

**Employer Account:**
- Email: `employer@example.com`
- Password: `password123`
- Role: Employer

### Test Workflows

1. **Job Seeker Workflow:**
   - Register as Job Seeker
   - Complete profile with skills and experience
   - Browse jobs
   - Apply for jobs
   - Track applications

2. **Employer Workflow:**
   - Register as Employer
   - Complete company profile
   - Post a job
   - Review applications
   - Update applicant status

3. **Theme Testing:**
   - Toggle dark/light mode
   - Verify colors change
   - Verify preference persists on refresh

## File Structure Overview

### Backend Files
- `server.js` - Main server entry point
- `config/db.js` - Database connection
- `models/` - MongoDB schemas
- `controllers/` - Business logic
- `routes/` - API endpoints
- `middleware/` - Auth and error handling

### Frontend Files
- `App.js` - Main React component
- `pages/` - Page components
- `components/` - Reusable components
- `hooks/` - Custom React hooks
- `context/` - React context providers
- `styles/` - CSS files
- `utils/api.js` - API client

## Useful Commands

### Backend
```bash
npm run dev      # Development server with auto-reload
npm start        # Production server
```

### Frontend
```bash
npm start        # Development server
npm run build    # Build for production
npm run test     # Run tests
```

## Common Issues & Solutions

### MongoDB Connection Error
**Problem:** Cannot connect to MongoDB
**Solution:**
1. Check connection string in .env
2. Verify IP in MongoDB Atlas whitelist
3. Ensure database name is correct

### Port Already in Use
**Problem:** Port 5000 or 3000 already in use
**Solution:**
```bash
# Find process using port 5000
lsof -i :5000
# Kill process
kill -9 <PID>

# Or change PORT in .env
PORT=5001
```

### CORS Error
**Problem:** Cannot call backend API
**Solution:**
1. Verify backend is running
2. Check REACT_APP_API_URL in .env
3. Verify CORS in server.js

### Module Not Found
**Problem:** Module dependency missing
**Solution:**
```bash
rm -rf node_modules
npm install
```

## Next Steps

1. **Customize Styling**
   - Edit CSS variables in `styles/global.css`
   - Modify color scheme
   - Add custom fonts

2. **Add Features**
   - Resume upload
   - Email notifications
   - Advanced search
   - Admin panel

3. **Optimize Performance**
   - Add caching
   - Optimize images
   - Minify bundles

4. **Deploy**
   - Follow DEPLOYMENT.md
   - Set up CI/CD
   - Configure domain

## Support

For issues or questions:
1. Check README.md in project root
2. Check backend/README.md
3. Check frontend/README.md
4. Review DEPLOYMENT.md for deployment issues

## Project Statistics

- **Backend APIs:** 15+ endpoints
- **Frontend Pages:** 7+ pages
- **Database Collections:** 3 (Users, Jobs, Applications)
- **Authentication:** JWT-based
- **Theme Support:** Dark mode & Light mode
- **Responsive:** Mobile & Desktop

Happy coding! 🚀
