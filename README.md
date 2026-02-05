# 🚀 CMSC 129 Laboratory Assign 1 Guide: Full-Stack CRUD Application

Author: Nikko Gabriel Hismaña

## 📋 Overview

Create a simple full-stack web application with CRUD (Create, Read, Update, Delete) operations using your preferred tech stack. You may choose from the following tech stacks:

- **MEAN** (MongoDB, Express.js, Angular, Node.js)
- **MERN** (MongoDB, Express.js, React, Node.js)
- **FEAN** (Firebase, Express.js, Angular, Node.js)
- **FERN** (Firebase, Express.js, React, Node.js)

## 🎯 Learning Objectives

- Understand full-stack web development principles
- Implement CRUD operations in a web application
- Work with modern JavaScript frameworks and libraries
- Practice database integration (MongoDB Atlas or Firebase)
- Learn REST API development with Express.js

## ✅ Application Requirements

Before you start, **create a GitHub repository** for your project named **"CMSC129-Lab1-LastNameFNInitials"** (e.g., CMSC129-Lab1-HismanaNG_AdenixK).

### Minimum Requirements

To get the passing score in the Features rubrics, your application must implement the following CRUD operations:

1. **Create**: Add new records to the database
2. **Read**: Display/retrieve records from the database
3. **Update**: Modify existing records
4. **Delete**: Remove records from the database (could be soft or hard delete)

Non-Functional Requirements:

1. **API Keys Visibility**: Your API Keys should _**not be exposed**_ in the frontend code or GitHub. Use environment variables or backend proxy to secure them. You can use "secret manager" packages like `dotenv` for Node.js applications. Whichever method you use, make sure that your API keys are not visible in the browser's developer tools, nor in your GitHub repository.
2. **Readme.md**: A comprehensive README file with installation instructions, usage guide, and documentation of your API endpoints. This should be seen in your GitHub repository.
3. **UX/UI**: Since you're done with CMSC134, I will hold your UX/UI design to a higher standard. (Will only affect your **Design Rubrics** score)

_NOTE: Testing or written tests is not required for this lab. But it can help you ensure that your application works as expected before the demo._

### Expanded Requirements

To get the perfect score in the Features Rubrics, your application must have the following:

1. **Soft Delete**: data is still in the database (can still be restored)
2. **Hard Delete**: data is purged/permanently deleted from the database
3. **Database Redundancy**: data should be backed up on a secondary database; during the demo, we disable your primary database and then we'll check if it retrieves data from your backup database.
   > **Example:**
   >
   > Primary database -> normal read/write
   >
   > Backup database -> copy of data, used for recovery
   >
   > In MERN, this usually means:
   >
   > MongoDB Atlas cluster#1 -> Primary
   >
   > MongoDB Atlas cluster#2 -> Backup
   >
   > Then your Node/Express backend connects to both, writes/updates to primary, and syncs to backup (either during every CRUD operation or timed)
   >
   > You can also try MongoDB (Primary) + Firebase (Backup) to learn the best practices in DB redundancy but this is not required

_NOTE: You have the freedom as to how you will implement these expanded requirements. Just make sure that they work as expected during the demo._

---

## 🛠️ Tech Stack Prerequisites

### Common Prerequisites (All Stacks)

- **Node.js** (v16.x or higher) - [Download](https://nodejs.org/)
- **npm** (comes with Node.js)
- **Git** - [Download](https://git-scm.com/)
- **Code Editor** (VS Code recommended) - [Download](https://code.visualstudio.com/)
- **Web Browser** (Chrome, Firefox, Safari, or Edge)

### 1. MEAN Stack Prerequisites

#### Required Software

1. **MongoDB Atlas** (cloud database) - [Create Free Account](https://www.mongodb.com/atlas)
   - **Note**: We will use MongoDB Atlas (cloud-based) only. Local MongoDB installation is not required.
2. **Angular CLI**
   ```bash
   npm install -g @angular/cli
   ```

#### Useful VS Code Extensions

- Angular Language Service
- MongoDB for VS Code
- Thunder Client (for API testing)

---

### 2. MERN Stack Prerequisites

#### Required Software

1. **MongoDB Atlas** (cloud database) - [Create Free Account](https://www.mongodb.com/atlas)
   - **Note**: We will use MongoDB Atlas (cloud-based) only. Local MongoDB installation is not required.

#### Useful VS Code Extensions

- ES7+ React/Redux/React-Native snippets
- MongoDB for VS Code
- Thunder Client (for API testing)

### 3. FEAN Stack Prerequisites

#### Required Software

1. **Firebase CLI**
   ```bash
   npm install -g firebase-tools
   ```
2. **Angular CLI**
   ```bash
   npm install -g @angular/cli
   ```

#### Setup Requirements

- Google/Firebase account - [Create account](https://firebase.google.com/)
- Firebase project setup

#### Useful VS Code Extensions

- Angular Language Service
- Firebase Explorer
- Thunder Client (for API testing)

### 4. FERN Stack Prerequisites

#### Required Software

1. **Firebase CLI**
   ```bash
   npm install -g firebase-tools
   ```

#### Setup Requirements

- Google/Firebase account - [Create account](https://firebase.google.com/)
- Firebase project setup

#### Useful VS Code Extensions

- ES7+ React/Redux/React-Native snippets
- Firebase Explorer
- Thunder Client (for API testing)

---

## 📁 Project Structure

These project structures are just guidelines. You can modify them as needed, but make sure to maintain a clear separation between frontend and backend code.

### MEAN/MERN Project Structure

```
project-name/
├── client/                 # Frontend (Angular/React)
│   ├── src/
│   ├── public/
│   ├── package.json
│   └── ...
├── server/                 # Backend (Express.js)
│   ├── models/            # Database models
│   ├── routes/            # API routes
│   ├── middleware/        # Custom middleware
│   ├── config/            # Database configuration
│   ├── server.js          # Main server file
│   └── package.json
├── README.md
└── .gitignore
```

### FEAN/FERN Project Structure

```
project-name/
├── client/                 # Frontend (Angular/React)
│   ├── src/
│   ├── public/
│   ├── package.json
│   └── ...
├── server/                 # Backend (Express.js)
│   ├── routes/            # API routes
│   ├── middleware/        # Custom middleware
│   ├── config/            # Firebase configuration
│   ├── server.js          # Main server file
│   └── package.json
├── firebase.json           # Firebase configuration
├── README.md
└── .gitignore
```

---

## 💻 Implementation Guide

_Disclaimer: This worked for me during my tests but you may need to adjust some parts based on your specific requirements and preferences._

### Phase 1: Backend Setup (Express.js + Database)

#### Step 1: Initialize Backend Project

```bash
mkdir your-project-name
cd your-project-name
mkdir server
cd server
npm init -y
```

#### Step 2: Install Backend Dependencies

**For MEAN/MERN (MongoDB Atlas):**

```bash
npm install express mongoose cors dotenv
npm install -D nodemon
```

**For FEAN/FERN (Firebase):**

```bash
npm install express firebase-admin cors dotenv
npm install -D nodemon
```

#### Step 3: Create Basic Server Structure

**server.js** (Common for all stacks):

```javascript
const express = require("express");
const cors = require("cors");
require("dotenv").config();

const app = express();
const PORT = process.env.PORT || 5000;

// Middleware
app.use(cors());
app.use(express.json());

// Routes
// TODO: Add your routes here

// Start server
app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});
```

#### Step 4: Database Configuration

**For MongoDB Atlas (MEAN/MERN):**

```javascript
const mongoose = require("mongoose");

const connectDB = async () => {
  try {
    await mongoose.connect(process.env.MONGODB_URI, {
      useNewUrlParser: true,
      useUnifiedTopology: true,
    });
    console.log("MongoDB Atlas connected");
  } catch (error) {
    console.error("MongoDB Atlas connection error:", error);
    process.exit(1);
  }
};

module.exports = connectDB;
```

**Note**: Create a `.env` file with your MongoDB Atlas connection string:

```
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/dbname?retryWrites=true&w=majority
```

**For Firebase (FEAN/FERN):**

```javascript
const admin = require("firebase-admin");
const serviceAccount = require("./path-to-service-account-key.json");

admin.initializeApp({
  credential: admin.credential.cert(serviceAccount),
  databaseURL: "your-firebase-database-url",
});

const db = admin.firestore();
module.exports = { admin, db };
```

#### Step 5: Create API Routes

Implement RESTful endpoints:

- `GET /api/items` - Get all items
- `GET /api/items/:id` - Get item by ID
- `POST /api/items` - Create new item
- `PUT /api/items/:id` - Update item
- `DELETE /api/items/:id` - Delete item

### Phase 2: Frontend Setup

#### For Angular (MEAN/FEAN):

```bash
cd .. # Go back to project root
ng new client
cd client
ng add @angular/material # Optional: for UI components
```

#### For React (MERN/FERN):

```bash
cd .. # Go back to project root
npx create-react-app client
cd client
npm install axios # for API calls
```

### Phase 3: Frontend Implementation

#### Required Components/Features:

1. **List View**: Display all items
2. **Add Form**: Create new items
3. **Edit Form**: Update existing items
4. **Delete Functionality**: Remove items
5. **Navigation**: User-friendly interface

#### API Integration:

- Use **Axios** (React; it's a promise-based HTTP client library making it easy to send requests such as GET, POST, PUT, DELETE) or **HttpClient** (Angular; built-in Angular service for making HTTP requests) to connect frontend with backend API endpoints.
- Implement error handling (always handle errors when making API calls)
- Add loading states (show users that something is happening while data is being fetched --- especially since Miagao internet is slow AF)

---

## 📤 Submission Requirements

### Deliverables

1. **F2F Demo and Defense**. Possible topics/concepts you'll be asked during the demo:
   - The architecture of your application (frontend, backend, database)
   - The tech stack you chose and why
   - How your tech stack is structured (i.e. Angular's modules, React's component hierarchy)
   - How you implemented CRUD operations
   - Hooks, components, services (for Angular/React)
   - How your database integration works (MongoDB Atlas or Firebase)
   - API endpoints and how they work
2. **GitHub Repository**. With complete source code and README.md

## 📊 RUBRICS FOR GRADING

### Grading Rubrics

![RUBRICS](/images/lab1rubrics.png)

## 📚 Helpful Resources

### Documentation

- [Node.js Documentation](https://nodejs.org/en/docs/)
- [Express.js Guide](https://expressjs.com/)
- [MongoDB Atlas Documentation](https://www.mongodb.com/docs/atlas/)
- [Mongoose Documentation](https://mongoosejs.com/docs/)
- [Firebase Documentation](https://firebase.google.com/docs)
- [Angular Documentation](https://angular.io/docs)
- [React Documentation](https://reactjs.org/docs)

### Tutorials

- [MEAN Stack Tutorial](https://www.mongodb.com/mean-stack)
- [MERN Stack Tutorial](https://www.mongodb.com/mern-stack)
- [MongoDB Atlas Setup Guide](https://www.mongodb.com/docs/atlas/getting-started/)
- [Firebase Web Tutorial](https://firebase.google.com/docs/web/setup)
- [Angular Tutorial](https://angular.io/tutorial)
- [React Tutorial](https://reactjs.org/tutorial/tutorial.html)
- For FERN/FEAN, combine Firebase tutorials with Angular/React tutorials
- _You can use YouTube tutorials as well, but from experience, some of the content may be outdated (i.e. deprecated packages, old versions of Angular/React, etc.) so make sure to check the date of the video and cross-reference with official documentation (add "2025" to your search query to get the latest results)._

### Tools

- [MongoDB Atlas](https://www.mongodb.com/atlas) - Cloud MongoDB Database
- [MongoDB Compass](https://www.mongodb.com/products/compass) - GUI for MongoDB
- [Postman](https://www.postman.com/) - API testing tool
- [Thunder Client](https://www.thunderclient.com/) - VS Code API testing extension
- [Firebase Console](https://console.firebase.google.com/) - Firebase management

---

## 💡 Support

If you encounter issues:

1. Check the console for error messages
2. Refer to official documentation
3. Search Stack Overflow for similar problems
4. Ask classmates for help
5. Contact the instructor during office hours
6. Use AI tools like ChatGPT or Claude for coding assistance (just make sure that you understand the code generated)
7. Pray.

**Good luck with your lab! 🚀**
![](images/lab1imp.gif)
