# Immunization Tracker - Windows Installation Guide

This guide will walk you through setting up the Immunization Tracker application on a Windows system.

## Prerequisites

Before you begin, ensure you have the following installed:

1. **Node.js** (version 14 or higher)
   - Download from: [https://nodejs.org/](https://nodejs.org/)
   - Choose the LTS (Long Term Support) version
   - Run the installer and follow the installation wizard

2. **MongoDB Community Edition**
   - Download from: [https://www.mongodb.com/try/download/community](https://www.mongodb.com/try/download/community)
   - Choose "Windows" as your platform
   - Run the installer and follow these steps:
     - Choose "Complete" installation
     - Check "Install MongoDB as a Service"
     - Keep the default data directory (C:\data\db)
     - Complete the installation

3. **Git** (optional, but recommended)
   - Download from: [https://git-scm.com/download/win](https://git-scm.com/download/win)
   - Run the installer with default settings

## Installation Steps

1. **Clone the Repository**
   ```bash
   git clone https://github.com/your-repository/immunization-tracker.git
   cd immunization-tracker
   ```
   Or download the ZIP file and extract it to your desired location.

2. **Install Dependencies**
   ```bash
   # Install backend dependencies
   cd backend
   npm install

   # Install frontend dependencies
   cd ../frontend
   npm install
   ```

3. **Configure MongoDB**
   - MongoDB should be running as a service after installation
   - To verify, open Command Prompt and run:
     ```bash
     mongod --version
     ```
   - If MongoDB isn't running, start it from Services:
     - Press `Windows + R`
     - Type `services.msc`
     - Find "MongoDB" in the list
     - Right-click and select "Start"

4. **Configure Environment Variables**
   Create a `.env` file in the backend directory with the following content:
   ```
   PORT=5000
   MONGODB_URI=mongodb://localhost:27017/immunization-tracker
   JWT_SECRET=your-secret-key
   ```

5. **Create Required Directories**
   ```bash
   # From the project root directory
   mkdir backend\uploads
   ```

## Running the Application

1. **Start the Backend Server**
   ```bash
   cd backend
   npm start
   ```
   The server should start on port 5000.

2. **Start the Frontend Development Server**
   ```bash
   cd frontend
   npm start
   ```
   The frontend should open automatically in your default browser at `http://localhost:3000`.

## Default Admin Account

After the first run, a default admin account will be created:
- Username: `admin`
- Password: `admin123`

**Important**: Change the admin password immediately after first login.

## Troubleshooting

### Common Issues

1. **MongoDB Connection Error**
   - Ensure MongoDB service is running
   - Check if the data directory exists (C:\data\db)
   - Verify the connection string in your .env file

2. **Port Already in Use**
   - If you see "EADDRINUSE" error, either:
     - Change the PORT in .env file
     - Find and close the process using that port

3. **Node.js Version Issues**
   - Verify Node.js version: `node --version`
   - Update if necessary using the Node.js installer

4. **Missing Dependencies**
   - Delete `node_modules` folder and `package-lock.json`
   - Run `npm install` again

## Security Notes

1. The application includes a login attempt lockout feature:
   - 3 failed attempts will lock the account for 15 minutes
   - Lockout resets on successful login

2. Always use strong passwords
3. Keep your JWT_SECRET secure and change it in production
4. Regularly backup your MongoDB database

## Support

For additional support or to report issues, please contact the development team or create an issue in the repository. 