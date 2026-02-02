# Chatbot Fix Guide

## Problem: Chatbot Not Working

If your chatbot is showing errors or not responding, follow these steps:

## Step 1: Fix Port Conflicts

**Multiple backend processes are running on port 5000!** This causes conflicts.

### Quick Fix (Windows):
1. Double-click `backend/fix_port_conflict.bat`
   - This will kill all processes on port 5000
   
2. Or manually:
   ```bash
   # Find processes on port 5000
   netstat -ano | findstr :5000
   
   # Kill each process (replace PID with actual process ID)
   taskkill /F /PID <PID>
   ```

### Manual Fix:
1. Open Task Manager (Ctrl+Shift+Esc)
2. Go to "Details" tab
3. Find Python processes
4. End all Python processes
5. Restart only ONE backend server

## Step 2: Restart Backend Server

1. **Stop all backend servers** (Ctrl+C in all terminals)

2. **Start ONE backend server:**
   ```bash
   cd backend
   python app.py
   ```

3. **Verify it's running:**
   - Should see: `Running on http://127.0.0.1:5000`
   - Open http://localhost:5000/api/health
   - Should show: `{"status":"healthy"}`

## Step 3: Test the Endpoint

Run the test script:
```bash
cd backend
python test_endpoint.py
```

This will test both health and chatbot endpoints.

## Step 4: Check Browser Console

1. Open your browser (F12)
2. Go to **Console** tab
3. Try sending a message
4. Look for error messages
5. Check **Network** tab to see the request/response

## Step 5: Verify Frontend Proxy

Make sure `vite.config.js` has:
```js
proxy: {
  '/api': {
    target: 'http://localhost:5000',
    changeOrigin: true
  }
}
```

Then restart frontend:
```bash
npm run dev
```

## Common Issues & Solutions

### Issue 1: "404 - Endpoint not found"
**Solution:** Backend server not running or route not registered
- Restart backend server
- Check backend terminal for errors
- Verify route exists in `backend/app.py`

### Issue 2: "Connection refused"
**Solution:** Backend server not running
- Start backend: `cd backend && python app.py`
- Check if port 5000 is available

### Issue 3: "CORS error"
**Solution:** CORS already configured, but restart both servers
- Restart backend
- Restart frontend
- Clear browser cache

### Issue 4: "Timeout error"
**Solution:** OpenAI API is slow or not responding
- Check internet connection
- Verify OpenAI API key in `.env` file
- Try again (OpenAI can be slow)

### Issue 5: Multiple processes on port 5000
**Solution:** Kill duplicate processes
- Run `backend/fix_port_conflict.bat`
- Or manually kill Python processes in Task Manager

## Debugging Steps

1. **Check backend logs:**
   - Look at the terminal where backend is running
   - You should see `[DEBUG]` messages when requests come in
   - Look for `[ERROR]` messages

2. **Test endpoints directly:**
   ```bash
   # Health check
   curl http://localhost:5000/api/health
   
   # Chatbot test
   curl -X POST http://localhost:5000/api/chatbot -H "Content-Type: application/json" -d "{\"message\":\"hello\",\"language\":\"en\"}"
   ```

3. **Check browser network tab:**
   - Open DevTools (F12)
   - Go to Network tab
   - Send a message
   - Check the request/response

## Still Not Working?

1. **Check Python version:**
   ```bash
   python --version
   ```
   Should be Python 3.8+

2. **Reinstall dependencies:**
   ```bash
   cd backend
   pip install -r requirements.txt
   ```

3. **Check .env file:**
   - Should be in `backend/.env`
   - Should contain: `OPENAI_API_KEY=your_key_here`
   - (Optional - works in demo mode without it)

4. **Check for syntax errors:**
   ```bash
   cd backend
   python -m py_compile app.py
   ```

5. **Try a different port:**
   - Change port in `backend/app.py` line 254 to `port=5001`
   - Update `vite.config.js` proxy target to `http://localhost:5001`
   - Restart both servers

## Expected Behavior

When working correctly:
- ✅ Health check shows "Connected" (green)
- ✅ Messages send successfully
- ✅ Bot responds (either with AI or demo responses)
- ✅ No errors in browser console
- ✅ Backend terminal shows `[DEBUG]` messages

## Quick Checklist

- [ ] Only ONE backend server running
- [ ] Backend shows "Running on http://127.0.0.1:5000"
- [ ] Health endpoint works: http://localhost:5000/api/health
- [ ] Frontend proxy configured correctly
- [ ] Browser console shows no errors
- [ ] Backend terminal shows request logs

