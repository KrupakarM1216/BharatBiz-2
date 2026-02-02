# Troubleshooting Guide - Chatbot Issues

## Common Issues and Solutions

### 1. Chatbot Not Responding / Connection Errors

**Symptoms:**
- Error message: "The backend server is not running"
- Status shows "Demo Mode" in orange
- Messages fail to send

**Solution:**
1. Make sure the Flask backend is running:
   ```bash
   cd backend
   python app.py
   ```
   You should see: `Running on http://127.0.0.1:5000`

2. Verify the backend is accessible:
   - Open http://localhost:5000/api/health in your browser
   - Should return: `{"status":"healthy"}`

3. Check that the frontend proxy is configured correctly in `vite.config.js`

### 2. OpenAI API Errors

**Symptoms:**
- Error message about API key
- "Authentication" errors
- 401 or 403 status codes

**Solution:**
1. Create `backend/.env` file:
   ```
   OPENAI_API_KEY=your_actual_api_key_here
   ```

2. Get your API key from: https://platform.openai.com/api-keys

3. Restart the Flask backend after adding the key

4. Verify the key is loaded:
   - Check backend console for "Warning: OPENAI_API_KEY not found" message
   - If you see this, the key is not being loaded

### 3. Network/CORS Errors

**Symptoms:**
- "Network Error" in console
- CORS errors in browser console

**Solution:**
1. Ensure backend CORS is enabled (already configured in `app.py`)

2. Check that frontend is running on port 3000 and backend on port 5000

3. Verify proxy configuration in `vite.config.js`:
   ```js
   proxy: {
     '/api': {
       target: 'http://localhost:5000',
       changeOrigin: true
     }
   }
   ```

### 4. Timeout Errors

**Symptoms:**
- "Request timed out" error
- Loading spinner never stops

**Solution:**
1. Check your internet connection
2. Verify OpenAI API is accessible
3. Try reducing `max_tokens` in backend if responses are too long

### 5. Demo Mode (No API Key)

**What it is:**
- The chatbot will work in demo mode without OpenAI API key
- Provides basic responses for common queries
- Shows "Demo Mode" status indicator

**To enable full AI:**
1. Add OpenAI API key to `backend/.env`
2. Restart backend server
3. Status will change to "Connected" (green)

## Testing the Setup

### Test Backend Connection:
```bash
curl http://localhost:5000/api/health
```

### Test Chatbot Endpoint:
```bash
curl -X POST http://localhost:5000/api/chatbot \
  -H "Content-Type: application/json" \
  -d '{"message": "Hello", "language": "en"}'
```

### Check Frontend Console:
- Open browser DevTools (F12)
- Check Console tab for errors
- Check Network tab for failed requests

## Quick Checklist

- [ ] Backend server is running (`python backend/app.py`)
- [ ] Frontend server is running (`npm run dev`)
- [ ] Backend is accessible at http://localhost:5000
- [ ] Frontend is accessible at http://localhost:3000
- [ ] `backend/.env` file exists with `OPENAI_API_KEY`
- [ ] No errors in browser console
- [ ] No errors in backend console

## Still Having Issues?

1. Check browser console for detailed error messages
2. Check backend console for Python errors
3. Verify all dependencies are installed:
   - Frontend: `npm install`
   - Backend: `pip install -r backend/requirements.txt`
4. Try restarting both servers
5. Clear browser cache and reload

