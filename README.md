# School Learning Management System (LMS)

A comprehensive online learning platform that replicates face-to-face educational experiences with comprehensive user management, course delivery, communication tools, and administrative controls.

## 🚀 Features

- **Multi-role System**: Super Admin, Principal, Teachers, and Students
- **Course Management**: Create, manage, and deliver courses with rich content
- **Video Integration**: Upload, stream, and manage educational videos
- **Live Classes**: Integrated video conferencing with interactive features
- **Assessment Tools**: Quizzes, assignments, and grading system
- **Communication**: Messaging, announcements, and discussion forums
- **Progress Tracking**: Monitor student progress and performance
- **Mobile Responsive**: Works on all devices

## 🛠 Tech Stack

### Frontend
- React.js with TypeScript
- Redux for state management
- Material-UI for UI components
- Video.js for video playback
- Socket.io for real-time features

### Backend
- Node.js with Express.js
- MongoDB with Mongoose
- JWT for authentication
- AWS S3 for file storage
- Redis for caching

## 🚀 Getting Started

### VPS Deployment (Quick Start)

1. **Upload the ZIP file to your VPS**
   ```bash
   # On your local machine
   scp school-lms.zip user@your_vps_ip:~/school-lms.zip
   ```

2. **SSH into your VPS and set up the project**
   ```bash
   # Connect to your VPS
   ssh user@your_vps_ip
   
   # Install required tools
   sudo apt-get update
   sudo apt-get install -y unzip docker.io docker-compose nginx
   
   # Create project directory and unzip
   mkdir -p ~/school-lms
   unzip ~/school-lms.zip -d ~/school-lms
   cd ~/school-lms
   
   # Set up environment variables
   cp .env.example .env
   nano .env  # Edit the configuration as needed
   
   # Set up Nginx (as root)
   sudo cp nginx/nginx.conf /etc/nginx/nginx.conf
   sudo cp nginx/school-lms.conf /etc/nginx/sites-available/
   sudo ln -s /etc/nginx/sites-available/school-lms.conf /etc/nginx/sites-enabled/
   sudo nginx -t  # Test configuration
   sudo systemctl restart nginx
   
   # Start the application
   docker-compose up -d --build
   
   # View logs
   docker-compose logs -f
   ```

3. **Set up SSL (optional but recommended)**
   ```bash
   sudo apt-get install -y certbot python3-certbot-nginx
   sudo certbot --nginx -d school.miolong.com
   ```

### Prerequisites

- Node.js (v16+)
- npm (v8+)
- MongoDB (v5+)
- Redis (v6+)
- Docker (for containerized deployment)

### Development Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/SLSTunnel/school-lms.git
   cd school-lms
   ```

2. **Install dependencies**
   ```bash
   # Install server dependencies
   cd server
   npm install
   
   # Install client dependencies
   cd ../client
   npm install
   ```

3. **Set up environment variables**
   - Copy `.env.example` to `.env` in both `server` and `client` directories
   - Update the variables with your configuration

4. **Start the development servers**
   ```bash
   # Start the backend server (from server directory)
   npm run dev
   
   # Start the frontend development server (from client directory)
   npm start
   ```

5. **Access the application**
   - Frontend: http://localhost:3000
   - Backend API: http://localhost:5000

## 🚀 Production Deployment

### Option 1: Docker Compose (Recommended)

1. **Set up your server**
   - Spin up a VPS (Ubuntu 20.04/22.04 recommended)
   - SSH into your server

2. **Install Docker and Docker Compose**
   ```bash
   # Run the setup script (from project root)
   chmod +x deploy.sh
   ./deploy.sh setup
   ```
   
   > **Note:** You may need to log out and log back in after this step

3. **Configure environment variables**
   ```bash
   # Copy the example environment file
   cp .env.example .env
   
   # Edit the environment file with your settings
   nano .env
   ```

4. **Deploy the application**
   ```bash
   # Start the deployment
   ./deploy.sh deploy
   ```

5. **Set up SSL (Optional but recommended)**
   - Make sure your domain points to your server's IP address
   - Update the `DOMAIN` variable in your `.env` file
   - Run the deployment again:
     ```bash
     ./deploy.sh deploy
     ```

### Option 2: Manual Deployment

1. **Set up your server**
   - Install Node.js, npm, MongoDB, and Nginx
   - Set up a reverse proxy with Nginx
   - Configure SSL with Let's Encrypt

2. **Deploy the application**
   ```bash
   # Clone the repository
   git clone https://github.com/SLSTunnel/school-lms.git
   cd school-lms
   
   # Install dependencies
   cd server
   npm install --production
   
   # Build the client
   cd ../client
   npm install
   npm run build
   
   # Copy build files to Nginx serving directory
   sudo cp -r build/* /var/www/html/
   
   # Start the server (using PM2 recommended)
   cd ../server
   npm install -g pm2
   pm2 start dist/index.js --name "school-lms"
   pm2 save
   pm2 startup
   ```

## 🔄 Updating the Application

To update to the latest version:

```bash
# Pull the latest changes
git pull

# Rebuild and restart the containers
./deploy.sh update
```

## 💾 Backing Up Data

Regular backups are recommended. To create a backup:

```bash
./deploy.sh backup
```

This will create a timestamped backup file in the `backups` directory.

## 🔄 Restoring from Backup

To restore from a backup:

```bash
./deploy.sh restore path/to/backup_file.tar.gz
```

## 🔧 Environment Variables

See `.env.example` for all available environment variables and their descriptions.

## 🤝 Contributing

1. Fork the repository
2. Create a new branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 📞 Support

For support, please open an issue in the GitHub repository.

## 🙏 Acknowledgments

- [MongoDB](https://www.mongodb.com/)
- [Express.js](https://expressjs.com/)
- [React](https://reactjs.org/)
- [Node.js](https://nodejs.org/)
- [Material-UI](https://mui.com/)
- [Docker](https://www.docker.com/)
- [Nginx](https://www.nginx.com/)
   # Install server dependencies
   cd server
   npm install
   
   # Install client dependencies
   cd ../client
   npm install
   ```

3. **Environment Setup**
   - Create `.env` files in both `server` and `client` directories
   - Configure environment variables (see `.env.example` files)

4. **Start Development Servers**
   ```bash
   # In server directory
   npm run dev
   
   # In client directory (new terminal)
   npm start
   ```

## 🔧 Environment Variables

### Server (`.env`)
```
NODE_ENV=development
PORT=5000
MONGODB_URI=mongodb://localhost:27017/school_lms
JWT_SECRET=your_jwt_secret
JWT_EXPIRE=30d
COOKIE_EXPIRE=30
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_EMAIL=your_email@gmail.com
SMTP_PASSWORD=your_email_password
AWS_ACCESS_KEY_ID=your_aws_access_key
AWS_SECRET_ACCESS_KEY=your_aws_secret_key
AWS_REGION=your_aws_region
AWS_BUCKET_NAME=your_bucket_name
```

### Client (`.env`)
```
REACT_APP_API_URL=http://localhost:5000/api/v1
REACT_APP_STRIPE_PUBLIC_KEY=your_stripe_public_key
```

## 🐳 Docker Setup

1. Install Docker and Docker Compose
2. Run the following command:
   ```bash
   docker-compose up --build
   ```
3. Access the application at `http://localhost:3000`

## 🚀 Deployment

### Prerequisites
- VPS (Ubuntu 20.04 recommended)
- Domain name (optional but recommended)
- SSH access to your VPS

### VPS Setup via SSH

1. **Connect to your VPS**
   ```bash
   ssh root@your_server_ip
   ```

2. **Update system packages**
   ```bash
   sudo apt update && sudo apt upgrade -y
   ```

3. **Install required software**
   ```bash
   # Install Node.js
   curl -fsSL https://deb.nodesource.com/setup_16.x | sudo -E bash -
   sudo apt install -y nodejs
   
   # Install MongoDB
   sudo apt install -y mongodb
   
   # Install Nginx
   sudo apt install -y nginx
   
   # Install PM2
   sudo npm install -g pm2
   ```

4. **Clone and deploy the application**
   ```bash
   git clone https://github.com/SLSTunnel/school-lms.git
   cd school-lms
   
   # Install dependencies
   cd server && npm install --production
   cd ../client && npm install --production
   
   # Build the React app
   npm run build
   ```

5. **Configure Nginx**
   ```bash
   sudo nano /etc/nginx/sites-available/school-lms
   ```
   
   Add the following configuration:
   ```nginx
   server {
       listen 80;
       server_name school.miolong.com www.school.miolong.com;
       
       location / {
           root /path/to/school-lms/client/build;
           try_files $uri /index.html;
       }
       
       location /api {
           proxy_pass http://localhost:5000;
           proxy_http_version 1.1;
           proxy_set_header Upgrade $http_upgrade;
           proxy_set_header Connection 'upgrade';
           proxy_set_header Host $host;
           proxy_cache_bypass $http_upgrade;
       }
   }
   ```

6. **Enable the site and restart Nginx**
   ```bash
   sudo ln -s /etc/nginx/sites-available/school-lms /etc/nginx/sites-enabled
   sudo nginx -t
   sudo systemctl restart nginx
   ```

7. **Start the application with PM2**
   ```bash
   cd /path/to/school-lms/server
   pm2 start server.js --name "school-lms"
   pm2 save
   pm2 startup
   ```

## 🔒 Security

- Use HTTPS with Let's Encrypt
- Implement rate limiting
- Use Helmet.js for securing Express
- Regular security audits
- Input validation and sanitization
- CORS configuration

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🤝 Contributing

1. Fork the project
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📧 Contact

Your Name - your.email@example.com

Project Link: [https://github.com/yourusername/school-lms](https://github.com/yourusername/school-lms)
