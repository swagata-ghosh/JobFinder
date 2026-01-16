# JobFinder - MERN Stack Job Portal

A comprehensive full-stack job portal application built with the MERN stack (MongoDB, Express.js, React.js, Node.js).

## Features

### For Job Seekers
- ✅ User registration and login with role-based authentication
- ✅ Complete profile management (skills, experience, resume)
- ✅ Browse and search job listings with advanced filters
- ✅ Apply for jobs with cover letters
- ✅ Track application status
- ✅ Save jobs for later
- ✅ View saved job applications

### For Employers/Recruiters
- ✅ Company profile creation and management
- ✅ Post, edit, and delete job listings
- ✅ Manage job postings dashboard
- ✅ Review and manage applications
- ✅ Update applicant status (Shortlisted, Interview, Offered, etc.)
- ✅ Add notes and ratings to applications
- ✅ Analytics dashboard (application counts, views)

### General Features
- ✅ Dark mode and light mode themes
- ✅ Responsive design for mobile and desktop
- ✅ Role-based access control
- ✅ Secure JWT authentication
- ✅ Advanced job search and filtering
- ✅ Pagination for job listings
- ✅ Real-time application status updates

## Tech Stack

### Frontend
- **React.js** - UI Library
- **React Router** - Client-side routing
- **Axios** - HTTP client
- **CSS** - Styling with CSS modules and custom themes
- **React Icons** - Icon library

### Backend
- **Node.js** - Runtime environment
- **Express.js** - Web framework
- **MongoDB** - NoSQL database
- **Mongoose** - MongoDB ODM
- **JWT** - Authentication
- **bcryptjs** - Password hashing
- **Multer** - File uploads
- **Express Validator** - Request validation

## Project Structure

```
jobfinder/
├── backend/
│   ├── config/
│   │   └── db.js                 # MongoDB configuration
│   ├── controllers/
│   │   ├── authController.js     # Authentication logic
│   │   ├── jobController.js      # Job management logic
│   │   └── applicationController.js # Application logic
│   ├── middleware/
│   │   ├── auth.js               # JWT authentication & authorization
│   │   └── errorHandler.js       # Global error handling
│   ├── models/
│   │   ├── User.js               # User schema
│   │   ├── Job.js                # Job schema
│   │   └── Application.js        # Application schema
│   ├── routes/
│   │   ├── auth.js               # Auth routes
│   │   ├── jobs.js               # Job routes
│   │   └── applications.js       # Application routes
│   ├── server.js                 # Main server file
│   ├── package.json
│   └── .env                      # Environment variables
│
└── frontend/
    ├── public/
    │   └── index.html
    ├── src/
    │   ├── components/
    │   │   └── Navbar.js         # Navigation component
    │   ├── context/
    │   │   ├── AuthContext.js    # Auth context provider
    │   │   └── ThemeContext.js   # Theme context provider
    │   ├── hooks/
    │   │   ├── useAuth.js        # Auth hook
    │   │   └── useTheme.js       # Theme hook
    │   ├── pages/
    │   │   ├── Home.js           # Home page
    │   │   ├── Login.js          # Login page
    │   │   ├── Register.js       # Registration page
    │   │   ├── JobListing.js     # Job listings page
    │   │   ├── JobDetails.js     # Job details page
    │   │   ├── Applications.js   # Applications page
    │   │   └── PostJob.js        # Post job page
    │   ├── styles/
    │   │   ├── global.css        # Global styles
    │   │   └── components.css    # Component styles
    │   ├── utils/
    │   │   └── api.js            # API client setup
    │   ├── App.js
    │   └── index.js
    ├── package.json
    └── .env
```

## Installation & Setup

### Prerequisites
- Node.js (v14+)
- npm or yarn
- MongoDB Atlas account (for cloud database) or local MongoDB

### Backend Setup

1. Navigate to backend directory:
```bash
cd backend
```

2. Install dependencies:
```bash
npm install
```

3. Create `.env` file with the following:
```env
PORT=5000
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/jobfinder
JWT_SECRET=your_secret_key_here_change_this
NODE_ENV=development
```

4. Start the server:
```bash
npm run dev
```

The backend will run on `http://localhost:5000`

### Frontend Setup

1. Navigate to frontend directory:
```bash
cd frontend
```

2. Install dependencies:
```bash
npm install
```

3. Create `.env` file:
```env
REACT_APP_API_URL=http://localhost:5000/api
```

4. Start the development server:
```bash
npm start
```

The frontend will run on `http://localhost:3000`

## API Endpoints

### Authentication Routes
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - Login user
- `GET /api/auth/me` - Get current user
- `PUT /api/auth/profile` - Update profile
- `PUT /api/auth/change-password` - Change password

### Job Routes
- `GET /api/jobs` - Get all jobs with filters
- `GET /api/jobs/:id` - Get single job
- `POST /api/jobs` - Create job (employer only)
- `PUT /api/jobs/:id` - Update job (employer only)
- `DELETE /api/jobs/:id` - Delete job (employer only)
- `GET /api/jobs/employer/my-jobs` - Get employer's jobs

### Application Routes
- `POST /api/applications/:jobId` - Apply for job (job seeker only)
- `GET /api/applications/my-applications` - Get job seeker's applications
- `GET /api/applications/employer/applications` - Get employer's applications
- `GET /api/applications/:applicationId` - Get single application
- `PUT /api/applications/:applicationId` - Update application status (employer only)
- `DELETE /api/applications/:applicationId` - Withdraw application (job seeker only)

## Database Schemas

### User Schema
```javascript
{
  name: String,
  email: String (unique),
  password: String (hashed),
  role: 'jobseeker' | 'employer',
  // Job Seeker Fields
  skills: [String],
  experience: Number,
  experienceLevel: String,
  resume: String (file path),
  bio: String,
  // Employer Fields
  companyName: String,
  companyWebsite: String,
  companyDescription: String,
  industry: String
}
```

### Job Schema
```javascript
{
  jobTitle: String,
  companyName: String,
  location: String,
  salaryMin: Number,
  salaryMax: Number,
  jobType: 'Full-time' | 'Part-time' | 'Remote' | 'Internship' | 'Contract',
  requiredSkills: [String],
  experienceLevel: String,
  description: String,
  responsibilities: [String],
  benefits: [String],
  applicationsCount: Number,
  viewsCount: Number,
  active: Boolean
}
```

### Application Schema
```javascript
{
  jobId: ObjectId (ref: Job),
  jobSeekerId: ObjectId (ref: User),
  employerId: ObjectId (ref: User),
  coverLetter: String,
  status: 'Applied' | 'Shortlisted' | 'Interview' | 'Offered' | 'Rejected',
  appliedDate: Date,
  notes: String,
  rating: Number (0-5)
}
```

## Key Features Implementation

### Authentication
- JWT-based authentication
- Bcrypt password hashing
- Role-based access control
- Protected routes with middleware

### Job Search & Filters
- Text search on job titles and descriptions
- Filter by location, salary range, job type, experience level
- Pagination support
- Full-text search indexes on MongoDB

### Job Management
- Create, read, update, delete operations
- Employer-specific job listings
- Application count tracking
- Job view statistics

### Applications
- Apply with cover letters
- Track application status
- Update status by employers
- Add notes and ratings
- Withdraw applications (job seekers)

### Theme Management
- Light and dark mode toggle
- Persistent theme preference using localStorage
- CSS variables for theme colors
- Smooth theme transitions

## Future Enhancements

- [ ] Resume file upload and storage
- [ ] Email notifications
- [ ] Job alerts and recommendations
- [ ] Advanced analytics for employers
- [ ] Video interview integration
- [ ] Admin panel for system management
- [ ] Social media login
- [ ] Company reviews and ratings
- [ ] Chatting system between employers and job seekers
- [ ] Job bookmarking/favorites
- [ ] Advanced search with AI recommendations

## Deployment

### MongoDB Atlas Setup
1. Create MongoDB Atlas account
2. Create a cluster
3. Get connection string
4. Update `.env` with connection string

### Frontend Deployment (Vercel)
1. Push code to GitHub
2. Connect repository to Vercel
3. Set environment variables
4. Deploy

### Backend Deployment (Heroku/Railway)
1. Set environment variables
2. Deploy using Git or CLI
3. Update frontend `.env` with backend URL

## Environment Variables

**Backend (.env)**
```env
PORT=5000
MONGODB_URI=mongodb+srv://user:password@cluster.mongodb.net/jobfinder
JWT_SECRET=your_secret_key_here
NODE_ENV=development
```

**Frontend (.env)**
```env
REACT_APP_API_URL=http://localhost:5000/api
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a pull request

## License

This project is licensed under the MIT License.

## Support

For support, email support@jobfinder.com or open an issue in the repository.

## Troubleshooting

### MongoDB Connection Error
- Ensure MongoDB connection string is correct
- Check IP whitelist in MongoDB Atlas
- Verify network connectivity

### CORS Errors
- Ensure backend is running on port 5000
- Check CORS configuration in server.js
- Verify frontend API URL in .env

### Port Already in Use
- Change PORT in backend .env
- Kill process using `npm run dev`

### Module Not Found
- Run `npm install` in both frontend and backend directories
- Clear node_modules and reinstall if needed

---

**Built with ❤️ for job seekers and employers worldwide**
