# Quick Start Guide

## Prerequisites
- Node.js 18+ installed
- Python 3.8+ installed
- OpenAI API key

## Setup Steps

### 1. Install Dependencies

**Frontend:**
```bash
npm install
```

**Backend:**
```bash
cd backend
pip install -r requirements.txt
```

### 2. Configure Environment

Create `backend/.env` file:
```
OPENAI_API_KEY=your_api_key_here
```

### 3. Run the Application

**Terminal 1 - Frontend:**
```bash
npm run dev
```
Frontend will run on http://localhost:3000

**Terminal 2 - Backend:**
```bash
cd backend
python app.py
```
Backend will run on http://localhost:5000

### 4. Access the Application

Open your browser and navigate to: http://localhost:3000

## Features to Test

1. **Onboarding**: First-time users will see an onboarding flow
2. **Language Toggle**: Click the globe icon to switch between English/Hindi
3. **Chatbot**: Navigate to Chatbot page and try asking questions
4. **Marketing Generator**: 
   - Select platform (WhatsApp/Instagram/Facebook)
   - Enter description
   - Generate content and poster
5. **Dashboard**: View sales analytics and AI recommendations

## Troubleshooting

- **Backend not connecting**: Ensure backend is running on port 5000
- **API errors**: Check your OpenAI API key in `.env` file
- **CORS errors**: Backend CORS is configured for localhost:3000

## Demo Mode

If OpenAI API is not configured, the app will use mock data for demonstration purposes.

