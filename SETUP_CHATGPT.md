# 🚀 URGENT: ChatGPT API Setup - NxtWave Buildathon

## ⚡ QUICK START (2 Minutes)

### Step 1: Create `.env` file

**Windows (PowerShell):**
```powershell
cd backend
echo "OPENAI_API_KEY=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" > .env
```

**Mac/Linux:**
```bash
cd backend
cat > .env << EOF
OPENAI_API_KEY=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
EOF
```

**OR Manual:**
1. Go to `backend/` folder
2. Create new file named `.env` (no extension)
3. Paste this line:
```
OPENAI_API_KEY=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
```

### Step 2: Install Dependencies

**Backend:**
```bash
cd backend
pip install openai flask-cors python-dotenv
```

**Frontend:**
```bash
npm install
```

### Step 3: Start Servers

**Terminal 1 - Backend:**
```bash
cd backend
python app.py
```
Should see: `Running on http://127.0.0.1:5000`

**Terminal 2 - Frontend:**
```bash
npm run dev
```
Should see: `Local: http://localhost:3000`

### Step 4: Test!

1. Open http://localhost:3000/chatbot
2. Try these test messages:

**English:** "What's my order status?"
**Hindi:** "Mera order status kya hai?"
**Kannada:** "ನನ್ನ ಆರ್ಡರ್ ಎಲ್ಲಿ?"
**Tamil:** "என் ஆர்டர் எங்கே?"
**Telugu:** "నా ఆర్డర్ స్థితి ఏమిటి?"

## ✅ What's Implemented

### Backend (`backend/app.py`)
- ✅ New `/api/chat` endpoint
- ✅ GPT-4o-mini integration
- ✅ 5-language support (en, hi, kn, ta, te)
- ✅ Error handling
- ✅ CORS enabled

### Frontend (`src/pages/Chatbot.jsx`)
- ✅ Beautiful gradient UI (Indigo to Orange)
- ✅ Real-time chat interface
- ✅ Language selector with flags
- ✅ Quick reply buttons
- ✅ Typing indicator
- ✅ Auto-scroll
- ✅ Enter to send
- ✅ Loading states
- ✅ Error handling

## 🎨 UI Features

- **Gradient Background**: `from-indigo-50 to-orange-50`
- **User Messages**: Indigo bubbles (right)
- **Bot Messages**: Green bubbles (left)
- **Language Selector**: Top-right dropdown
- **Quick Replies**: Bottom buttons
- **Typing Animation**: "BharatBiz is typing..."

## 🧪 Test Checklist

- [ ] Backend running on port 5000
- [ ] Frontend running on port 3000
- [ ] `.env` file exists in `backend/` folder
- [ ] API key is correct in `.env`
- [ ] Can send messages in English
- [ ] Can switch languages
- [ ] Bot responds in selected language
- [ ] Quick reply buttons work
- [ ] Typing indicator shows
- [ ] Messages auto-scroll

## 🐛 Troubleshooting

### "API key not found"
- Check `.env` file is in `backend/` folder
- Restart backend after creating `.env`
- Verify no extra spaces in API key

### "Connection refused"
- Make sure backend is running: `python backend/app.py`
- Check port 5000 is not in use

### "Messages not sending"
- Open browser console (F12)
- Check Network tab for errors
- Verify `/api/chat` endpoint is accessible

## 🎯 Demo Script for Judges

1. **Show Language Selector**: "We support 5 Indian languages"
2. **Switch to Kannada**: Select ಕನ್ನಡ from dropdown
3. **Type**: "ನನ್ನ ಆರ್ಡರ್ ಎಲ್ಲಿ?"
4. **Show Response**: Bot responds in Kannada
5. **Show Quick Replies**: Click "ಆರ್ಡರ್ ಸ್ಥಿತಿ?"
6. **Switch to Tamil**: Show Tamil interface
7. **Generate Marketing**: Show multilingual content generation

## 📝 API Endpoint Details

**URL:** `POST /api/chat`

**Request:**
```json
{
  "message": "What's my order status?",
  "language": "en"
}
```

**Response:**
```json
{
  "success": true,
  "message": "Your order #1234 is being processed...",
  "isBot": true
}
```

## 🚀 Ready to Demo!

Everything is set up and working. Just:
1. Create `.env` file
2. Start both servers
3. Test the chatbot!

**Good luck with the Buildathon! 🎉**

