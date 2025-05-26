# 📋 Collaborative Coding Platform - Project Documentation

## 🎯 Project Overview

### What is this project?
This is a **real-time collaborative coding platform** that allows multiple developers to work together on coding projects simultaneously, similar to Google Docs but for code. The platform includes an integrated AI assistant powered by Google's Gemini AI for intelligent code generation and suggestions.

### Key Capabilities:
- 👥 **Real-time collaboration** - Multiple users can edit code simultaneously
- 🤖 **AI-powered assistance** - Get code suggestions and generation using `@ai` commands
- 🌐 **Live code execution** - Run and preview applications directly in the browser
- 💬 **Team communication** - Built-in chat for collaborators
- 📁 **Project management** - Organize files and manage team access

---

## 🏗️ System Architecture

### High-Level Architecture:
```
┌─────────────────┐    HTTP/WebSocket    ┌─────────────────┐
│                 │ ◄─────────────────► │                 │
│   Frontend      │                     │    Backend      │
│   (React App)   │                     │   (Node.js)     │
│                 │                     │                 │
└─────────────────┘                     └─────────┬───────┘
                                                  │
                                        ┌─────────▼───────┐
                                        │                 │
                                        │   Databases     │
                                        │ MongoDB + Redis │
                                        │                 │
                                        └─────────────────┘
                                                  │
                                        ┌─────────▼───────┐
                                        │                 │
                                        │  Google Gemini  │
                                        │   AI Service    │
                                        │                 │
                                        └─────────────────┘
```

### Communication Flow:
1. **Frontend** sends HTTP requests for CRUD operations
2. **WebSocket** connections handle real-time collaboration
3. **Backend** processes requests and manages data
4. **MongoDB** stores persistent data (users, projects, files)
5. **Redis** handles caching and session management
6. **Google AI** provides intelligent code assistance

---

## 🛠️ Technology Stack

### Frontend Technologies:
| Technology | Version | Purpose |
|------------|---------|---------|
| **React** | 18.3.1 | UI framework for building interactive interfaces |
| **Vite** | 6.0.1 | Fast build tool and development server |
| **Tailwind CSS** | 3.4.16 | Utility-first CSS framework for styling |
| **Socket.io Client** | 4.8.1 | Real-time communication with backend |
| **Axios** | 1.7.9 | HTTP client for API requests |
| **React Router DOM** | 7.0.2 | Client-side routing and navigation |
| **Highlight.js** | 11.11.0 | Syntax highlighting for code editor |
| **WebContainer API** | 1.5.1 | Browser-based development environment |

### Backend Technologies:
| Technology | Version | Purpose |
|------------|---------|---------|
| **Node.js** | Latest | JavaScript runtime environment |
| **Express.js** | 4.21.2 | Web application framework |
| **MongoDB** | Latest | NoSQL database for data storage |
| **Mongoose** | 8.8.4 | MongoDB object modeling library |
| **Socket.io** | 4.8.1 | Real-time bidirectional communication |
| **JWT** | 9.0.2 | JSON Web Token for authentication |
| **bcrypt** | 5.1.1 | Password hashing and security |
| **Google Generative AI** | 0.21.0 | AI integration for code assistance |
| **Redis (ioredis)** | 5.4.1 | Caching and session management |

---

## 📁 Project Structure

```
Agents/
├── backend/                    # Backend Node.js application
│   ├── controllers/           # Request handlers
│   │   ├── user.controller.js
│   │   ├── project.controller.js
│   │   └── ai.controller.js
│   ├── models/               # Database schemas
│   │   ├── user.model.js
│   │   └── project.model.js
│   ├── routes/               # API route definitions
│   │   ├── user.routes.js
│   │   ├── project.routes.js
│   │   └── ai.routes.js
│   ├── services/             # Business logic
│   │   ├── user.service.js
│   │   ├── project.service.js
│   │   ├── ai.service.js
│   │   └── redis.service.js
│   ├── middleware/           # Custom middleware
│   │   └── auth.middleware.js
│   ├── db/                   # Database configuration
│   │   └── db.js
│   ├── app.js               # Express app configuration
│   ├── server.js            # Server entry point
│   └── package.json         # Dependencies and scripts
│
├── frontend/                  # Frontend React application
│   ├── src/
│   │   ├── components/       # Reusable UI components
│   │   ├── screens/          # Page components
│   │   ├── routes/           # Routing configuration
│   │   ├── context/          # React context providers
│   │   ├── auth/             # Authentication logic
│   │   ├── config/           # Configuration files
│   │   ├── assets/           # Static assets
│   │   ├── App.jsx           # Main app component
│   │   └── main.jsx          # Application entry point
│   ├── public/               # Public static files
│   ├── package.json          # Dependencies and scripts
│   ├── vite.config.js        # Vite configuration
│   └── tailwind.config.js    # Tailwind CSS configuration
│
├── DFD.md                    # Data Flow Diagram documentation
├── ER_Diagram.md             # Entity-Relationship Diagram
├── README.md                 # Project overview and setup
└── PROJECT_DOCUMENTATION.md  # This comprehensive guide
```

---

## 🔧 Development Environment Setup

### Prerequisites:
- **Node.js** (v16 or higher) - JavaScript runtime
- **npm** or **yarn** - Package manager
- **MongoDB** - Database (local or MongoDB Atlas)
- **Redis** - Caching server
- **Google AI API Key** - For AI integration

### Installation Steps:

#### 1. Clone and Setup Backend:
```bash
cd backend
npm install
```

#### 2. Create Environment File (.env):
```env
PORT=3000
MONGODB_URI=mongodb://localhost:27017/collaborative-coding
JWT_SECRET=your-super-secret-jwt-key-here
GOOGLE_AI_KEY=your-google-ai-api-key-here
REDIS_URL=redis://localhost:6379
```

#### 3. Setup Frontend:
```bash
cd frontend
npm install
```

#### 4. Start Development Servers:
```bash
# Terminal 1 - Backend
cd backend
npm start

# Terminal 2 - Frontend  
cd frontend
npm run dev
```

### Access URLs:
- **Frontend**: http://localhost:5173
- **Backend API**: http://localhost:3000

---

## 🔐 Authentication & Security

### Authentication Flow:
1. User registers/logs in with email and password
2. Password is hashed using bcrypt before storage
3. JWT token is generated and sent to client
4. Token is stored in browser and sent with each request
5. Backend middleware validates token for protected routes

### Security Features:
- **Password Hashing**: bcrypt with salt rounds
- **JWT Tokens**: Secure authentication tokens
- **CORS**: Cross-origin resource sharing protection
- **Input Validation**: express-validator for request validation
- **Session Management**: Redis for token blacklisting

---

## 📊 Database Design

### MongoDB Collections:

#### Users Collection:
```javascript
{
  _id: ObjectId,
  email: String (unique),
  password: String (hashed),
  username: String,
  createdAt: Date,
  updatedAt: Date
}
```

#### Projects Collection:
```javascript
{
  _id: ObjectId,
  projectName: String (unique),
  description: String,
  users: [ObjectId], // Array of user IDs
  fileTree: Object,  // File structure
  createdAt: Date,
  updatedAt: Date
}
```

### Redis Cache:
- JWT token blacklist
- Session data
- Temporary AI responses
- Real-time collaboration state

---

## 🚀 Key Features Explained

### 1. Real-time Collaboration
- **Technology**: Socket.io WebSocket connections
- **How it works**: Users join project "rooms" and broadcast code changes
- **Implementation**: Event-driven architecture with real-time synchronization

### 2. AI Code Assistant
- **Technology**: Google Gemini AI API
- **Trigger**: Type `@ai` followed by your request
- **Features**: Code generation, debugging help, explanations
- **Processing**: Natural language → AI API → Formatted response

### 3. Live Code Execution
- **Technology**: WebContainer API
- **Capability**: Run Node.js applications in browser
- **Benefits**: No server-side execution needed, secure sandboxing

### 4. File Management
- **Structure**: Tree-based file organization
- **Storage**: MongoDB with JSON file tree structure
- **Operations**: Create, read, update, delete files and folders

---

## 🔄 API Endpoints

### Authentication Endpoints:
- `POST /users/register` - Create new user account
- `POST /users/login` - Authenticate user
- `GET /users/profile` - Get current user info
- `GET /users/all` - List all users

### Project Management:
- `POST /projects/create` - Create new project
- `GET /projects/get-project/:id` - Get project details
- `PUT /projects/add-user` - Add collaborator
- `PUT /projects/update-file-tree` - Update files

### AI Integration:
- `POST /ai/generate` - Generate AI responses

---

## 🎮 How to Use the Platform

### For New Team Members:

#### 1. Getting Started:
- Register an account with email/password
- Login to access the dashboard
- Create a new project or join existing one

#### 2. Collaborative Coding:
- Open project in the code editor
- See real-time changes from other collaborators
- Use file tree to navigate project structure
- Save changes automatically

#### 3. AI Assistance:
- Type `@ai` in chat followed by your request
- Examples:
  - `@ai create a React component for user login`
  - `@ai debug this JavaScript function`
  - `@ai explain this code snippet`

#### 4. Team Communication:
- Use built-in chat to communicate
- See who's online and actively coding
- Share ideas and coordinate work

---

## 🐛 Common Issues & Solutions

### Development Issues:

#### MongoDB Connection Error:
```bash
# Check if MongoDB is running
sudo systemctl status mongod

# Start MongoDB
sudo systemctl start mongod
```

#### Redis Connection Error:
```bash
# Check Redis status
redis-cli ping

# Start Redis
sudo systemctl start redis
```

#### AI Not Responding:
- Verify Google AI API key in .env file
- Check API quota and billing
- Ensure internet connection

#### WebContainer Issues:
- Use modern browser (Chrome, Firefox, Safari)
- Enable WebAssembly support
- Clear browser cache

---

## 👥 Team Collaboration Guidelines

### Code Standards:
- Use ES6+ JavaScript features
- Follow React functional component patterns
- Implement proper error handling
- Write descriptive commit messages

### Git Workflow:
1. Create feature branches from main
2. Make small, focused commits
3. Test changes before pushing
4. Create pull requests for review
5. Merge after approval

### Communication:
- Use project chat for quick questions
- Document major changes
- Share knowledge with team members
- Report bugs and issues promptly

---

## 📈 Future Enhancements

### Planned Features:
- **Version Control**: Git integration
- **Code Review**: Built-in review system
- **Testing**: Automated testing framework
- **Deployment**: One-click deployment
- **Mobile App**: Mobile development support
- **Video Chat**: Integrated video calls
- **Plugin System**: Extensible architecture

---

## 📞 Support & Contact

### Development Team:
- **Umashankar Singh** - umassingh@gmail.com
- **Abhay Singh** - as9450638@gmail.com  
- **Sakshi Sachan** - sakshisachan30@gmail.com
- **Abhinav Maurya** - abinav804546@gmail.com

### Getting Help:
1. Check this documentation first
2. Search existing issues in repository
3. Ask team members in project chat
4. Create new issue with detailed description
5. Contact development team directly

---
