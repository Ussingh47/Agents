# Agents
This project is a Group Work AI IDE designed to facilitate real-time collaborative coding for multiple users. Built with a focus on security and privacy,All participants can work simultaneously on the same project, enabling seamless collaboration, efficient teamwork, and synchronized updates.

# Collaborative Coding Platform with AI Assistant(Agents)

A real-time collaborative coding platform that allows multiple developers to work together on projects with integrated AI assistance powered by Google's Gemini AI. The platform features a web-based code editor, file management, live preview, and intelligent code generation.

## 🚀 Features

- **Real-time Collaboration**: Multiple users can work on the same project simultaneously
- **AI-Powered Code Generation**: Integrated Gemini AI assistant for code suggestions and generation
- **Live Code Editor**: Syntax-highlighted code editor with real-time updates
- **Web Container Integration**: Run and preview applications directly in the browser
- **Project Management**: Create, manage, and share coding projects
- **User Authentication**: Secure user registration and login system
- **File Tree Management**: Organize and navigate project files easily
- **Live Chat**: Communicate with collaborators in real-time
- **Responsive Design**: Works seamlessly across different screen sizes

## 🛠️ Tech Stack

### Frontend
- **React 18** - Modern UI library
- **Vite** - Fast build tool and development server
- **Tailwind CSS** - Utility-first CSS framework
- **Socket.io Client** - Real-time communication
- **Axios** - HTTP client for API requests
- **React Router DOM** - Client-side routing
- **Highlight.js** - Syntax highlighting
- **Markdown-to-JSX** - Markdown rendering
- **WebContainer API** - Browser-based development environment

### Backend
- **Node.js** - JavaScript runtime
- **Express.js** - Web application framework
- **MongoDB** - NoSQL database
- **Mongoose** - MongoDB object modeling
- **Socket.io** - Real-time bidirectional communication
- **JWT** - JSON Web Token authentication
- **bcrypt** - Password hashing
- **Google Generative AI** - AI integration
- **Redis** - Caching and session management

## 📋 Prerequisites

Before running this project, make sure you have the following installed:

- **Node.js** (v16 or higher)
- **npm** or **yarn**
- **MongoDB** (local installation or MongoDB Atlas)
- **Redis** (for caching)
- **Google AI API Key** (for Gemini AI integration)

## 🚀 Installation

### 1. Clone the Repository

```bash
git clone <repository-url>
cd Agents
```

### 2. Backend Setup

```bash
cd backend
npm install
```

Create a `.env` file in the backend directory:

```env
PORT=3000
MONGODB_URI=mongodb://localhost:27017/collaborative-coding
JWT_SECRET=your-super-secret-jwt-key
GOOGLE_AI_KEY=your-google-ai-api-key
REDIS_URL=redis://localhost:6379
```

### 3. Frontend Setup

```bash
cd ../frontend
npm install
```

### 4. Start the Application

#### Start Backend Server
```bash
cd backend
npm start
```

#### Start Frontend Development Server
```bash
cd frontend
npm run dev
```

The application will be available at:
- Frontend: `http://localhost:5173`
- Backend: `http://localhost:3000`

## ⚙️ Configuration

### Environment Variables

#### Backend (.env)
- `PORT` - Server port (default: 3000)
- `MONGODB_URI` - MongoDB connection string
- `JWT_SECRET` - Secret key for JWT token generation
- `GOOGLE_AI_KEY` - Google AI API key for Gemini integration
- `REDIS_URL` - Redis connection URL

### Google AI Setup

1. Visit [Google AI Studio](https://makersuite.google.com/app/apikey)
2. Create a new API key
3. Add the API key to your `.env` file as `GOOGLE_AI_KEY`

## 🎯 Usage

1. **Register/Login**: Create an account or login with existing credentials
2. **Create Project**: Start a new coding project
3. **Invite Collaborators**: Add team members to your project
4. **Code Together**: Use the real-time editor to write code collaboratively
5. **AI Assistance**: Type `@ai` followed by your request to get AI-powered code suggestions
6. **Live Preview**: Run your application and see live results in the integrated browser
7. **Chat**: Communicate with your team using the built-in chat feature

## 📡 API Endpoints

### Authentication
- `POST /users/register` - User registration
- `POST /users/login` - User login
- `GET /users/profile` - Get user profile
- `GET /users/all` - Get all users

### Projects
- `POST /projects/create` - Create new project
- `GET /projects/get-project/:id` - Get project details
- `PUT /projects/add-user` - Add collaborator to project
- `PUT /projects/update-file-tree` - Update project file structure

### AI Integration
- `POST /ai/generate` - Generate AI responses

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the ISC License.

## 🐛 Troubleshooting

### Common Issues

1. **MongoDB Connection Error**: Ensure MongoDB is running and the connection string is correct
2. **Redis Connection Error**: Make sure Redis server is running
3. **AI Not Responding**: Verify your Google AI API key is valid and has sufficient quota
4. **WebContainer Issues**: Ensure you're using a modern browser that supports WebAssembly

## 📞 Support

For support and questions, please open an issue in the repository or contact the development team.

Umashankar Singh (umassingh@gmail.com)
Abhay Singh (as9450638@gmail.com)
Sakshi Sachan (sakshisachan30@gmail.com)
Abhinav Maurya (abinav804546@gamil.com)

Built with ❤️ by the development team

