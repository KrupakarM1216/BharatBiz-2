# Fix: 404 Error on Chatbot Endpoint

## Problem
- Health check shows "Connected" ✅
- But chatbot messages return 404 error ❌

## Solution Steps

### Step 1: Restart the Backend Server
The most common cause is that the backend server needs to be restarted:

1. **Stop the backend server** (press `Ctrl+C` in the terminal where it's running)

2. **Restart it:**
   ```bash
   cd backend
   python app.py
   ```

3. **Verify it's running:**
   - You should see: `Running on http://127.0.0.1:5000`
   - Open http://localhost:5000/api/health in your browser
   - Should show: `{"status":"healthy"}`

### Step 2: Test the Chatbot Endpoint Directly

Open your browser and test:
- http://localhost:5000/api/test
- Should show: `{"status":"success","method":"GET","message":"Backend is working correctly!"}`

### Step 3: Check Browser Console

1. Open your browser's Developer Tools (F12)
2. Go to the **Console** tab
3. Try sending a message in the chatbot
4. Look for any error messages
5. Check the **Network** tab to see the actual request/response

### Step 4: Verify Proxy Configuration

Make sure `vite.config.js` has:
```js
proxy: {
  '/api': {
    target: 'http://localhost:5000',
    changeOrigin: true
  }
}
```

### Step 5: Restart Frontend Server

If backend restart doesn't work, restart the frontend too:

1. Stop the frontend (Ctrl+C)
2. Restart it:
   ```bash
   npm run dev
   ```

### Step 6: Clear Browser Cache

1. Hard refresh: `Ctrl+Shift+R` (Windows) or `Cmd+Shift+R` (Mac)
2. Or clear browser cache and reload

## Still Not Working?

Check the backend terminal for errors. Common issues:

1. **Port 5000 already in use:**
   - Change port in `backend/app.py` line 235 to `port=5001`
   - Update `vite.config.js` proxy target to `http://localhost:5001`

2. **Python/Flask not installed:**
   ```bash
   cd backend
   pip install -r requirements.txt
   ```

3. **Module import errors:**
   - Make sure you're in the correct Python environment
   - Reinstall dependencies: `pip install -r requirements.txt`

## Quick Test Commands

Test backend directly (in a new terminal):
```bash
# Test health endpoint
curl http://localhost:5000/api/health

# Test chatbot endpoint
curl -X POST http://localhost:5000/api/chatbot -H "Content-Type: application/json" -d "{\"message\":\"hello\",\"language\":\"en\"}"
```

If these work but the frontend doesn't, it's a proxy/frontend issue.
If these don't work, it's a backend issue.

