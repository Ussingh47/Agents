# Data Flow Diagram (DFD) - Collaborative Coding Platform

## System Overview

This document presents the Data Flow Diagram for the Collaborative Coding Platform with AI Assistant. The system enables real-time collaborative coding with integrated AI assistance, project management, and live code execution.

## DFD Levels

### Level 0 - Context Diagram

```
┌─────────────────┐    User Registration/Login     ┌─────────────────────────────┐
│                 │ ──────────────────────────────►│                             │
│                 │                                │                             │
│   Collaborators │    Project Data & Messages     │   Collaborative Coding      │
│   (Users)       │ ◄─────────────────────────────►│     Platform                │
│                 │                                │                             │
│                 │    Real-time Collaboration     │                             │
└─────────────────┘ ◄─────────────────────────────►└─────────────────────────────┘
                                                                    │
                                                                    │ AI Requests
                                                                    ▼
                                                    ┌─────────────────────────────┐
                                                    │                             │
                                                    │   Google Gemini AI          │
                                                    │   Service                   │
                                                    │                             │
                                                    └─────────────────────────────┘
```

### Level 1 - System Overview

```
┌─────────────┐
│ Users       │
│ (External   │
│ Entity)     │
└──────┬──────┘
       │
       │ 1. Authentication Data
       ▼
┌─────────────────────────────────────────────────────────────────────────────────┐
│                           COLLABORATIVE CODING PLATFORM                         │
│                                                                                 │
│  ┌─────────────┐  2. User Data   ┌─────────────┐  3. Project Data  ┌──────────┐ │
│  │   1.0       │ ──────────────► │    D1       │ ◄──────────────── │   2.0    │ │
│  │ Authenticate│                 │   Users     │                   │ Manage   │ │
│  │   User      │ ◄────────────── │ Database    │ ──────────────►   │ Projects │ │
│  └─────────────┘  User Profile   └─────────────┘  User Projects    └──────────┘ │
│         │                                                              │        │
│         │ Auth Token                                                   │        │
│         ▼                                                              │        │
│  ┌─────────────┐  4. Real-time   ┌─────────────┐  5. File Data    ┌──────────┐  │
│  │    3.0      │ ──────────────► │    D2       │ ◄─────────────── │   4.0    │  │
│  │ Handle      │   Messages      │  Projects   │   File Tree      │ Manage   │  │
│  │ Real-time   │ ◄────────────── │ Database    │ ──────────────►  │ Files    │  │
│  │Collaboration│   Project Info  └─────────────┘   Project Files  └──────────┘  │
│  └─────────────┘                                                       │        │
│         │                                                              │        │
│         │ 6. AI Request                                                │        │
│         ▼                                                              │        │
│  ┌─────────────┐  7. AI Response ┌─────────────┐  8. Session Data ┌──────────┐  │
│  │    5.0      │ ◄────────────── │    D3       │ ◄────────────────│   6.0    │  │
│  │ Process AI  │                 │   Redis     │   Token Cache    │ Manage   │  │
│  │ Requests    │ ──────────────► │   Cache     │ ──────────────►  │ Sessions │  │
│  └─────────────┘  Cache AI Data  └─────────────┘   Auth Tokens    └──────────┘  │
│         │                                                                       │
│         │ 9. AI Query                                                           │
│         ▼                                                                       │
└─────────────────────────────────────────────────────────────────────────────────┘
         │
         │ 10. AI Processing
         ▼
┌─────────────────┐
│ Google Gemini   │
│ AI Service      │
│ (External)      │
└─────────────────┘
```

### Level 2 - Detailed Process Breakdown

#### 2.1 Authentication Process (Process 1.0)

```
┌─────────────┐
│ User Login/ │
│ Register    │
│ Request     │
└──────┬──────┘
       │
       ▼
┌─────────────┐    Validate     ┌─────────────┐    Hash        ┌─────────────┐
│    1.1      │ ──────────────► │    1.2      │ ──────────────►│    1.3      │
│ Validate    │   Credentials   │ Hash        │   Password     │ Generate    │
│ Input       │                 │ Password    │                │ JWT Token   │
└─────────────┘                 └─────────────┘                └─────────────┘
       │                               │                               │
       │ Validation Error              │ Hashed Password               │ JWT Token
       ▼                               ▼                               ▼
┌─────────────┐                ┌─────────────┐                ┌─────────────┐
│    D1       │                │    D1       │                │    D3       │
│ Users       │ ◄───────────── │ Users       │ ─────────────► │ Redis       │
│ Database    │   User Data    │ Database    │   Store Token  │ Cache       │
└─────────────┘                └─────────────┘                └─────────────┘
```

#### 2.2 Project Management Process (Process 2.0)

```
┌─────────────┐
│ Project     │
│ Operations  │
│ Request     │
└──────┬──────┘
       │
       ▼
┌─────────────┐    Project     ┌─────────────┐    Update      ┌─────────────┐
│    2.1      │ ─────────────► │    2.2      │ ─────────────► │    2.3      │
│ Create/     │   Data         │ Validate    │   Project      │ Manage      │
│ Update      │                │ Project     │   Info         │Collaborators│
│ Project     │                │ Data        │                │             │
└─────────────┘                └─────────────┘                └─────────────┘
       │                               │                               │
       │ Project Info                  │ Validated Data                │ User List
       ▼                               ▼                               ▼
┌─────────────┐                ┌─────────────┐                ┌─────────────┐
│    D2       │ ◄──────────────│    D2       │ ────────────►  │    D1       │
│ Projects    │   Project Data │ Projects    │   User IDs     │ Users       │
│ Database    │                │ Database    │                │ Database    │
└─────────────┘                └─────────────┘                └─────────────┘
```

#### 2.3 Real-time Collaboration Process (Process 3.0)

```
┌─────────────┐
│ Socket      │
│ Connection  │
│ & Messages  │
└──────┬──────┘
       │
       ▼
┌─────────────┐    Auth        ┌─────────────┐    Broadcast   ┌─────────────┐
│    3.1      │ ─────────────► │    3.2      │ ─────────────► │    3.3      │
│ Authenticate│   Token        │ Join        │   Messages     │ Handle      │
│ Socket      │                │ Project     │                │ Messages    │
│ Connection  │                │ Room        │                │             │
└─────────────┘                └─────────────┘                └─────────────┘
       │                               │                               │
       │ User Info                     │ Room ID                       │ Message Data
       ▼                               ▼                               ▼
┌─────────────┐                ┌─────────────┐                ┌─────────────┐
│    D1       │                │ Socket.io   │                │ Connected   │
│ Users       │                │ Rooms       │                │ Clients     │
│ Database    │                │ (Memory)    │                │ (Memory)    │
└─────────────┘                └─────────────┘                └─────────────┘
```

#### 2.4 AI Processing (Process 5.0)

```
┌─────────────┐
│ AI Request  │
│ (@ai        │
│ message)    │
└──────┬──────┘
       │
       ▼
┌─────────────┐    Extract     ┌─────────────┐    Process     ┌─────────────┐
│    5.1      │ ─────────────► │    5.2      │ ─────────────► │    5.3      │
│ Parse AI    │   Prompt       │ Call        │   AI Response  │ Format      │
│ Request     │                │ Gemini AI   │                │ Response    │
└─────────────┘                └─────────────┘                └─────────────┘
       │                               │                               │
       │ Parsed Prompt                 │ AI Query                      │ Formatted Response
       ▼                               ▼                               ▼
┌─────────────┐                ┌─────────────┐                ┌─────────────┐
│ Message     │                │ Google      │                │ Project     │
│ Buffer      │                │ Gemini AI   │                │ Room        │
│ (Memory)    │                │ (External)  │                │ (Socket.io) │
└─────────────┘                └─────────────┘                └─────────────┘
```

## Data Stores

### D1 - Users Database (MongoDB)
- **Purpose**: Store user account information
- **Data Elements**:
  - User ID (ObjectId)
  - Email (String, unique)
  - Password (Hashed String)
  - Created Date
  - Updated Date

### D2 - Projects Database (MongoDB)
- **Purpose**: Store project information and file structures
- **Data Elements**:
  - Project ID (ObjectId)
  - Project Name (String, unique)
  - Users Array (ObjectId references)
  - File Tree (Object)
  - Created Date
  - Updated Date

### D3 - Redis Cache
- **Purpose**: Store session tokens and temporary data
- **Data Elements**:
  - JWT Tokens (for blacklisting)
  - Session Data
  - Temporary AI responses
  - Cache expiration times

### D4 - Socket.io Memory Store
- **Purpose**: Manage real-time connections and rooms
- **Data Elements**:
  - Socket connections
  - Room memberships
  - Active user sessions
  - Message queues

## External Entities

### 1. Users/Collaborators
- **Role**: Primary system users
- **Interactions**:
  - Register/Login
  - Create/Join projects
  - Send messages and code
  - Request AI assistance

### 2. Google Gemini AI Service
- **Role**: External AI service provider
- **Interactions**:
  - Receive code generation requests
  - Return AI-generated responses
  - Process natural language prompts

## Data Flows

### Primary Data Flows:
1. **Authentication Flow**: User credentials → Validation → JWT Token
2. **Project Flow**: Project data → Storage → Collaboration
3. **Real-time Flow**: Messages → Broadcasting → All collaborators
4. **AI Flow**: User prompt → AI processing → Generated response
5. **File Flow**: Code changes → File tree update → Persistence

### Security Data Flows:
- JWT token validation
- Password hashing
- Session management
- Token blacklisting

This DFD represents the complete data flow architecture of the collaborative coding platform, showing how data moves through the system from user interactions to AI processing and real-time collaboration.
