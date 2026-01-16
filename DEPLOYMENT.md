# MERN Job Portal - Deployment Guide

## Pre-Deployment Checklist

- [ ] Test all features locally
- [ ] Update environment variables
- [ ] Run security audit
- [ ] Optimize images and assets
- [ ] Test across browsers
- [ ] Enable HTTPS
- [ ] Set up database backups

## Database Setup (MongoDB Atlas)

### 1. Create MongoDB Atlas Account
- Go to https://www.mongodb.com/cloud/atlas
- Sign up or login
- Create a new project

### 2. Create a Cluster
- Select "Create a Database"
- Choose cloud provider (AWS, GCP, or Azure)
- Select region (choose closest to users)
- Choose cluster tier (M0 Free tier for development)

### 3. Configure Access
- Add IP address to whitelist (or allow all: 0.0.0.0/0)
- Create database user with strong password
- Note the connection string

### 4. Create Collections
- Collections are created automatically when data is inserted
- Create indexes for better performance

### 5. Connection String
```
mongodb+srv://username:password@cluster.mongodb.net/jobfinder?retryWrites=true&w=majority
```

## Backend Deployment (Node.js)

### Option 1: Deploy to Heroku

1. **Install Heroku CLI**
```bash
npm install -g heroku
```

2. **Login to Heroku**
```bash
heroku login
```

3. **Create Heroku App**
```bash
heroku create your-app-name
```

4. **Set Environment Variables**
```bash
heroku config:set PORT=5000
heroku config:set MONGODB_URI=your_mongodb_connection_string
heroku config:set JWT_SECRET=your_secret_key
heroku config:set NODE_ENV=production
```

5. **Deploy**
```bash
git push heroku main
```

### Option 2: Deploy to Railway

1. Go to https://railway.app
2. Connect GitHub repository
3. Create new project
4. Add MongoDB plugin
5. Set environment variables
6. Deploy

### Option 3: Deploy to DigitalOcean

1. Create a Droplet (Ubuntu 20.04)
2. SSH into droplet
3. Install Node.js and npm
4. Clone repository
5. Install dependencies
6. Set up environment variables
7. Use PM2 to manage process
8. Set up Nginx as reverse proxy

## Frontend Deployment (React)

### Option 1: Deploy to Vercel

1. **Push code to GitHub**
```bash
git add .
git commit -m "Final version"
git push origin main
```

2. **Go to Vercel**
- Visit https://vercel.com
- Sign up with GitHub
- Import your repository
- Set environment variables:
```
REACT_APP_API_URL=https://your-backend-url/api
```
- Deploy

### Option 2: Deploy to Netlify

1. **Build the project**
```bash
npm run build
```

2. **Deploy to Netlify**
- Go to https://netlify.com
- Sign in with GitHub
- Choose your repository
- Set build command: `npm run build`
- Set publish directory: `build`
- Deploy

3. **Configure environment variables**
- Go to Site settings
- Add environment variables
- Trigger rebuild

### Option 3: Deploy to Firebase Hosting

1. **Install Firebase CLI**
```bash
npm install -g firebase-tools
```

2. **Initialize Firebase**
```bash
firebase init hosting
```

3. **Build and Deploy**
```bash
npm run build
firebase deploy
```

## Environment Variables Configuration

### Backend (.env)
```env
PORT=5000
MONGODB_URI=mongodb+srv://user:password@cluster.mongodb.net/jobfinder
JWT_SECRET=production_secret_key_very_long_random_string
NODE_ENV=production
```

### Frontend (.env)
```env
REACT_APP_API_URL=https://your-backend-url/api
```

## Post-Deployment Steps

1. **Test the application**
   - Test registration and login
   - Test job posting
   - Test job applications
   - Test all filters

2. **Monitor performance**
   - Set up error tracking (Sentry)
   - Monitor database performance
   - Track API response times

3. **Enable HTTPS**
   - Vercel: Automatic
   - Heroku: Automatic
   - Custom: Use Let's Encrypt

4. **Set up backups**
   - MongoDB Atlas: Automatic daily backups
   - Schedule weekly manual backups

5. **Configure CDN**
   - Use CloudFlare for caching
   - Improve load times globally

## Optimization Tips

### Frontend Optimization
```bash
# Analyze bundle size
npm run build -- --analyze

# Add service worker
npm install workbox-cli

# Minify and compress assets
```

### Backend Optimization
- Add caching (Redis)
- Implement rate limiting
- Optimize database queries
- Use load balancing

## Security Considerations

1. **Environment Variables**
   - Never commit .env files
   - Use strong JWT_SECRET
   - Rotate secrets regularly

2. **HTTPS**
   - Always use HTTPS in production
   - Enable HSTS headers

3. **Database Security**
   - Enable IP whitelist
   - Use strong passwords
   - Enable authentication
   - Regular backups

4. **API Security**
   - Implement rate limiting
   - Add CORS properly
   - Validate all inputs
   - Use helmet for headers

5. **Code Security**
   - Run npm audit regularly
   - Keep dependencies updated
   - Use security linters
   - Regular code reviews

## Monitoring and Logging

### Error Tracking
- Sentry: https://sentry.io
- Bugsnag: https://bugsnag.com
- Rollbar: https://rollbar.com

### Performance Monitoring
- New Relic: https://newrelic.com
- DataDog: https://datadoghq.com
- Elastic: https://elastic.co

### Logging
```javascript
// Backend
npm install winston

// Frontend
npm install @sentry/react
```

## Troubleshooting Deployment

### Frontend Won't Load
- Check build output
- Verify API URL in .env
- Check browser console for errors
- Clear cache and rebuild

### Backend Connection Issues
- Verify MongoDB connection string
- Check IP whitelist
- Verify environment variables
- Check firewall rules

### CORS Errors
- Verify CORS configuration
- Check backend URL in frontend
- Verify API endpoint URLs

### Database Connection Timeout
- Check MongoDB Atlas status
- Verify IP whitelist
- Check connection string
- Check network connectivity

## Rollback Plan

### If deployment fails:

1. **Identify the issue**
```bash
# Check logs
heroku logs --tail
```

2. **Rollback to previous version**
```bash
# Heroku
heroku releases
heroku rollback v<number>

# Git
git revert HEAD
git push origin main
```

3. **Fix the issue locally**
4. **Test thoroughly**
5. **Redeploy**

## Performance Benchmarks

Expected metrics for production:
- Frontend load time: < 3 seconds
- API response time: < 200ms
- Database query time: < 50ms
- Uptime: 99.9%

## Support and Maintenance

- Regular security updates
- Weekly backups
- Monthly performance review
- Quarterly optimization
- Annual full security audit
