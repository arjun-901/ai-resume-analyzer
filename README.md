Author - Arjun Maurya 

# AI Resume Analyzer - Database & API Summary

## 📊 Project Overview
**Project Name:** AI Resume Analyzer  
**Type:** Full-stack React application with TypeScript  
**Framework:** React Router v7, React 19, Vite  
**Hosting/Runtime:** Node.js (Alpine)

---

## 🗄️ DATABASE USED

### **Puter.js KV (Key-Value Store)**
- **Type:** Key-Value Database (NoSQL)
- **Provider:** Puter.js platform
- **Usage:** Store resume data and feedback

#### Data Structure Stored:
```typescript
Key Format: "resume:{uuid}"
Value: {
  id: string;
  resumePath: string;
  imagePath: string;
  companyName: string;
  jobTitle: string;
  jobDescription: string;
  feedback: Feedback object;
}
```

#### KV Operations Used:
- `kv.get(key)` - Retrieve resume data by key
- `kv.set(key, value)` - Store resume data
- `kv.delete(key)` - Delete resume data
- `kv.list(pattern)` - List all resumes matching pattern
- `kv.flush()` - Clear all data

---

## 🔌 APIs USED

### 1. **Puter.js Authentication API**
- **Provider:** Puter.js
- **Purpose:** User authentication and account management
- **Endpoints:**
  - `auth.getUser()` - Get current authenticated user
  - `auth.isSignedIn()` - Check if user is signed in
  - `auth.signIn()` - Sign in user
  - `auth.signOut()` - Sign out user

### 2. **Puter.js File System API**
- **Provider:** Puter.js
- **Purpose:** Upload, store, and retrieve files
- **Endpoints:**
  - `fs.write(path, data)` - Write file to filesystem
  - `fs.read(path)` - Read file from filesystem
  - `fs.upload(files)` - Upload files to cloud
  - `fs.delete(path)` - Delete files
  - `fs.readdir(path)` - List directory contents

### 3. **Puter.js AI API (LLM)**
- **Provider:** Puter.js (Claude 3.7 Sonnet model)
- **Purpose:** Resume analysis and feedback generation
- **Endpoints:**
  - `ai.chat(prompt, options)` - Send text/file to AI for analysis
  - `ai.feedback(path, message)` - Specialized function for resume feedback
  - `ai.img2txt(image)` - Extract text from images
  
#### AI Model Used:
- **Model:** Claude 3.7 Sonnet
- **Used For:** 
  - Analyzing resume PDFs
  - Generating structured feedback (JSON)
  - Evaluating ATS compatibility
  - Providing improvement suggestions

### 4. **PDF.js API**
- **Provider:** Mozilla (pdfjs-dist v5.3.93)
- **Purpose:** PDF rendering and conversion
- **Usage:** Convert PDF files to images for display

### 5. **Google Fonts API**
- **Provider:** Google
- **Purpose:** Load font "Inter"
- **Endpoint:** `https://fonts.googleapis.com/css2`

---

## 🗂️ FILE STORAGE

### Puter.js File System
Files are stored in Puter.js cloud storage with two types:
1. **Resume Files** - Original PDF files uploaded by user
2. **Image Files** - Converted resume images (from PDF to IMG)

---

## 📝 DATA FLOW SUMMARY

```
User Upload
    ↓
1. File uploaded to Puter FS
2. PDF converted to Image
3. Image uploaded to Puter FS
4. Resume data + paths stored in KV with UUID
5. PDF + paths sent to Claude 3.7 Sonnet AI
6. AI generates structured feedback (JSON)
7. Feedback stored in KV with resume data
8. User redirected to review page
9. Data retrieved from KV for display
```

---

## 🔑 Authentication & Authorization
- **Method:** Puter.js Authentication
- **Flow:** 
  - User must sign in to access upload and review features
  - Authentication state managed via Zustand store
  - Protected routes require authentication check

---

## 💾 Key Technical Stack

| Component | Technology | Version |
|-----------|-----------|---------|
| Runtime | Node.js | 20 (Alpine) |
| Frontend Framework | React | 19.1.0 |
| Routing | React Router | 7.5.3 |
| State Management | Zustand | 5.0.6 |
| TypeScript | TypeScript | 5.8.3 |
| Build Tool | Vite | 6.3.3 |
| Styling | Tailwind CSS | 4.1.4 |
| File Upload | react-dropzone | 14.3.8 |
| PDF Processing | pdfjs-dist | 5.3.93 |
| Backend Services | Puter.js | v2 |

---

## 🎯 External Dependencies
- **Puter.js** - Complete backend (Auth, FS, KV, AI)
- **Claude API** (via Puter.js) - AI analysis
- **Google Fonts** - Typography

---

## ✅ No Traditional Databases
This project **does NOT use**:
- ❌ PostgreSQL, MySQL, MongoDB
- ❌ Firebase Realtime Database
- ❌ Traditional SQL databases
- ❌ Custom backend REST API

Instead, it fully leverages **Puter.js** as an all-in-one backend platform.

---

## 📍 Resume Analysis Feedback Format

The AI generates structured feedback with these categories:
1. **Overall Score** (0-100)
2. **ATS Score** - Applicant Tracking System compatibility
3. **Tone & Style** - Writing quality evaluation
4. **Content** - Content relevance and quality
5. **Structure** - Resume layout and organization
6. **Skills** - Skills section evaluation

Each category includes multiple tips marked as "good" or "improve".
