# Immunization Tracker - Technical Documentation

## Architecture Overview

The application follows a modern full-stack architecture with:

- **Frontend**: React.js single-page application
- **Backend**: Node.js/Express.js REST API
- **Database**: MongoDB for data persistence
- **Authentication**: JWT-based authentication system

## Project Structure

```
immunization-tracker/
├── backend/
│   ├── server.js           # Main server file
│   ├── models/             # MongoDB models
│   ├── routes/             # API routes
│   ├── middleware/         # Custom middleware
│   ├── uploads/            # File upload directory
│   └── .env               # Environment variables
└── frontend/
    ├── src/
    │   ├── components/     # React components
    │   ├── pages/         # Page components
    │   ├── services/      # API service calls
    │   ├── context/       # React context
    │   ├── hooks/         # Custom hooks
    │   └── utils/         # Utility functions
    └── public/            # Static assets
```

## Backend Architecture

### Server Configuration
- Express.js server running on port 5000
- CORS enabled for cross-origin requests
- JSON body parsing middleware
- JWT authentication middleware
- File upload handling with Multer

### Database Models

1. **User Model**
```javascript
{
  username: String,
  password: String (hashed),
  isAdmin: Boolean,
  failedLoginAttempts: Number,
  lockoutUntil: Date
}
```

2. **Record Model**
```javascript
{
  userId: ObjectId,
  vaccineName: String,
  dateAdministered: Date,
  documentPath: String,
  uploadDate: Date
}
```

### API Endpoints

1. **Authentication**
   - `POST /api/register` - User registration
   - `POST /api/login` - User login with JWT token

2. **Records**
   - `POST /api/records` - Create new immunization record
   - `GET /api/records` - Get all records (admin) or user-specific records
   - `PUT /api/records/:id` - Update record
   - `DELETE /api/records/:id` - Delete record

### Security Features

1. **Password Security**
   - Bcrypt hashing for password storage
   - Minimum password requirements
   - Password reset functionality

2. **Authentication**
   - JWT-based authentication
   - Token expiration (1 hour)
   - Secure token storage

3. **Login Protection**
   - 3 failed attempts lockout
   - 15-minute lockout duration
   - Automatic lockout reset on successful login

## Frontend Architecture

### Component Structure

1. **Layout Components**
   - `App.js` - Main application wrapper
   - `Navbar.js` - Navigation component
   - `Sidebar.js` - Admin sidebar

2. **Page Components**
   - `Login.js` - Authentication page
   - `Dashboard.js` - Main dashboard
   - `Records.js` - Record management
   - `Admin.js` - Admin interface

3. **Reusable Components**
   - `RecordForm.js` - Record creation/editing
   - `RecordList.js` - Record display
   - `FileUpload.js` - Document upload

### State Management

1. **Context API**
   - `AuthContext` - Authentication state
   - `RecordContext` - Record management state

2. **Custom Hooks**
   - `useAuth` - Authentication logic
   - `useRecords` - Record management
   - `useForm` - Form handling

### API Integration

1. **Service Layer**
   - `authService.js` - Authentication API calls
   - `recordService.js` - Record API calls
   - `fileService.js` - File upload handling

2. **Error Handling**
   - Global error boundary
   - API error handling
   - Form validation

## Data Flow

1. **Authentication Flow**
   ```
   User Input → Frontend Validation → API Call → Backend Validation → 
   Database Check → Token Generation → Frontend Storage → Protected Routes
   ```

2. **Record Management Flow**
   ```
   User Action → Form Validation → API Call → Backend Processing → 
   Database Operation → Response → Frontend Update → UI Refresh
   ```

## Security Implementation

1. **Backend Security**
   - Input validation
   - SQL injection prevention
   - XSS protection
   - CSRF protection
   - Rate limiting

2. **Frontend Security**
   - Secure token storage
   - Input sanitization
   - Protected routes
   - Session management

## Performance Considerations

1. **Backend Optimization**
   - Database indexing
   - Query optimization
   - Caching strategies
   - File upload handling

2. **Frontend Optimization**
   - Code splitting
   - Lazy loading
   - Image optimization
   - State management

## Error Handling

1. **Backend Errors**
   - HTTP status codes
   - Error middleware
   - Logging system
   - Error responses

2. **Frontend Errors**
   - Error boundaries
   - User feedback
   - Error logging
   - Recovery mechanisms

## Testing Strategy

1. **Backend Testing**
   - Unit tests
   - Integration tests
   - API tests
   - Security tests

2. **Frontend Testing**
   - Component tests
   - Integration tests
   - E2E tests
   - Performance tests

## Deployment Considerations

1. **Environment Setup**
   - Production configuration
   - Environment variables
   - Database setup
   - File storage

2. **Monitoring**
   - Error tracking
   - Performance monitoring
   - User analytics
   - Security monitoring

## Maintenance

1. **Regular Tasks**
   - Database backups
   - Security updates
   - Dependency updates
   - Performance monitoring

2. **Documentation**
   - API documentation
   - Code documentation
   - User guides
   - Maintenance guides 