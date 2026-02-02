# How to Start the Backend Server

## Quick Start

The 404 error you're seeing means the **backend server is not running**. Follow these steps:

### Step 1: Open a Terminal/Command Prompt

### Step 2: Navigate to the Backend Directory
```bash
cd backend
```

### Step 3: Install Dependencies (if not already done)
```bash
pip install -r requirements.txt
```

### Step 4: Create .env File (if not exists)
Create a file named `.env` in the `backend` folder with:
```
OPENAI_API_KEY=your_api_key_here
```

**Note:** You can run without the API key in demo mode, but you'll need it for full AI functionality.

### Step 5: Start the Backend Server
```bash
python app.py
```

You should see:
```
 * Running on http://127.0.0.1:5000
```

### Step 6: Keep This Terminal Open
The backend must stay running. Don't close this terminal window.

### Step 7: In Another Terminal, Start the Frontend
```bash
npm run dev
```

## Verify It's Working

1. Open your browser and go to: http://localhost:5000/api/health
   - Should show: `{"status":"healthy"}`

2. Then go to: http://localhost:3000
   - The chatbot should now work!

## Common Issues

### Port 5000 Already in Use
If you see "Address already in use", another process is using port 5000:
- Windows: Find and close the process using port 5000
- Or change the port in `backend/app.py` (line 235) to a different port like 5001

### Module Not Found Errors
Make sure all dependencies are installed:
```bash
cd backend
pip install -r requirements.txt
```

### Still Getting 404?
1. Make sure the backend terminal shows "Running on http://127.0.0.1:5000"
2. Check that you're accessing http://localhost:3000 (not 5000)
3. Restart both frontend and backend servers

