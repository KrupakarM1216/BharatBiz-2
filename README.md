# BharatBiz.AI - AI-Powered Assistant for Local Indian Businesses

A modern web application designed to empower local Indian businesses with AI-powered customer support, marketing content generation, and sales analytics.

## Features

- 🤖 **Customer Support Chatbot**: 24/7 AI-powered support in multiple languages
- 📱 **AI Marketing Generator**: Create engaging posts for WhatsApp, Instagram, and Facebook with auto-generated images
- 📊 **Sales & Inventory Dashboard**: Real-time insights and AI-powered recommendations
- 🌐 **Multilingual Support**: Hindi and English (expandable to more languages)
- 📱 **Responsive Design**: Mobile-first, works on all devices
- 🎨 **Modern UI**: Clean, professional interface with intuitive navigation

## Tech Stack

### Frontend
- React 18
- Vite
- Tailwind CSS
- React Router
- Recharts (for dashboard visualizations)
- Lucide React (icons)

### Backend
- Flask
- OpenAI API (GPT-4o, DALL·E 3)
- Flask-CORS

## Getting Started

### Prerequisites
- Node.js (v18 or higher)
- Python 3.8 or higher
- OpenAI API key

### Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd BharatBiz-AI2
   ```

2. **Install frontend dependencies**
   ```bash
   npm install
   ```

3. **Install backend dependencies**
   ```bash
   cd backend
   pip install -r requirements.txt
   ```

4. **Set up environment variables**
   ```bash
   cd backend
   cp .env.example .env
   # Edit .env and add your OPENAI_API_KEY
   ```

5. **Run the development servers**

   Terminal 1 (Frontend):
   ```bash
   npm run dev
   ```

   Terminal 2 (Backend):
   ```bash
   cd backend
   python app.py
   ```

6. **Open your browser**
   Navigate to `http://localhost:3000`

## Project Structure

```
BharatBiz-AI2/
├── src/
│   ├── components/
│   │   ├── Navbar.jsx
│   │   └── Onboarding.jsx
│   ├── contexts/
│   │   └── LanguageContext.jsx
│   ├── pages/
│   │   ├── Home.jsx
│   │   ├── Chatbot.jsx
│   │   ├── Marketing.jsx
│   │   └── Dashboard.jsx
│   ├── App.jsx
│   ├── main.jsx
│   └── index.css
├── backend/
│   ├── app.py
│   ├── requirements.txt
│   └── .env.example
├── package.json
├── vite.config.js
├── tailwind.config.js
└── README.md
```

## API Endpoints

- `POST /api/chatbot` - Chatbot conversation
- `POST /api/marketing/text` - Generate marketing text content
- `POST /api/marketing/image` - Generate marketing poster image
- `GET /api/dashboard` - Get sales data and recommendations
- `GET /api/health` - Health check

## Features in Detail

### 1. Customer Support Chatbot
- Interactive chat interface
- AI-powered responses using GPT-4o
- Multi-language support
- Real-time messaging

### 2. Marketing Content Generator
- Platform selection (WhatsApp, Instagram, Facebook)
- Content type selection (Post, Promotion, Announcement)
- Auto-generated text content
- AI-generated promotional posters using DALL·E 3
- Copy and download functionality

### 3. Sales Dashboard
- Weekly sales trends (bar chart)
- Orders trend (line chart)
- Key metrics cards
- AI-powered business recommendations
- Low stock alerts

### 4. Multilingual Support
- Toggle between English and Hindi
- Persistent language preference
- All UI elements translated

## Deployment

### Frontend (Vercel)
1. Push code to GitHub
2. Import project in Vercel
3. Build command: `npm run build`
4. Output directory: `dist`

### Backend (Replit/Railway/Heroku)
1. Set environment variables
2. Deploy Flask app
3. Update CORS settings for production domain

## Future Enhancements

- [ ] Google Sheets integration for real sales data
- [ ] Voice support with Whisper API
- [ ] Text-to-speech for responses
- [ ] More regional languages (Tamil, Telugu, Bengali)
- [ ] User authentication
- [ ] Multiple business profiles
- [ ] Email marketing integration

## License

MIT License

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Support

For issues and questions, please open an issue on GitHub.

