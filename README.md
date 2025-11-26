# 🚀 MERN Stack + Airtable Dynamic Form Builder

> A full-stack application that allows users to create custom forms using Airtable data, with OAuth authentication, conditional logic, and real-time webhook synchronization.

## ✨ Features

- ✅ **Airtable OAuth Login** - Secure authentication with Airtable
- 📋 **Dynamic Form Builder** - Create forms from Airtable bases/tables/fields
- 🎯 **Conditional Logic** - Show/hide questions based on user answers
- 💾 **Dual Storage** - Save responses to both Airtable and MongoDB
- 🔄 **Webhook Sync** - Real-time updates when Airtable data changes
- 🎨 **Supported Field Types**: Text, Long Text, Single Select, Multi Select, Attachments

## 🛠️ Tech Stack

**Backend:**
- Node.js + Express
- MongoDB + Mongoose
- Airtable OAuth 2.0 + REST API
- JWT Authentication

**Frontend:**
- React 18 + Vite
- React Router
- Axios

## 📦 Installation

### Prerequisites
- Node.js 18+ 
- MongoDB running locally or MongoDB Atlas
- Airtable account

### Step 1: Clone Repository
```bash
git clone https://github.com/Samarth-27/mern-airtable-form-builder.git
cd mern-airtable-form-builder
```

### Step 2: Backend Setup
```bash
cd backend
npm install
```

Create `.env` file:
```env
PORT=5000
MONGODB_URI=mongodb://localhost:27017/airtable-form-builder
JWT_SECRET=your_super_secret_jwt_key

AIRTABLE_CLIENT_ID=your_client_id
AIRTABLE_CLIENT_SECRET=your_client_secret
AIRTABLE_REDIRECT_URI=http://localhost:5000/api/auth/airtable/callback

FRONTEND_URL=http://localhost:5173
WEBHOOK_SECRET=your_webhook_secret
```

### Step 3: Frontend Setup
```bash
cd ../frontend
npm install
```

### Step 4: Run the Application

**Terminal 1 (Backend):**
```bash
cd backend
npm run dev
```

**Terminal 2 (Frontend):**
```bash
cd frontend
npm run dev
```

Open **http://localhost:5173** in your browser.

## 🔑 Airtable OAuth Setup

1. Go to [Airtable Developer Hub](https://airtable.com/create/oauth)
2. Click **Register an OAuth integration**
3. Fill in:
   - **Name**: Dynamic Form Builder App
   - **Redirect URL**: `http://localhost:5000/api/auth/airtable/callback`
4. Select scopes:
   - `data.records:read`
   - `data.records:write`
   - `schema.bases:read`
5. Copy **Client ID** and **Client Secret** to your `.env` file

## 📚 API Documentation

### Authentication
- `GET /api/auth/airtable` - Initiate OAuth flow
- `GET /api/auth/airtable/callback` - OAuth callback
- `GET /api/auth/me` - Get current user

### Airtable Integration
- `GET /api/airtable/bases` - Get user's Airtable bases
- `GET /api/airtable/bases/:baseId/tables` - Get tables in a base
- `GET /api/airtable/bases/:baseId/tables/:tableId/fields` - Get supported fields

### Forms
- `POST /api/forms` - Create new form
- `GET /api/forms` - Get all user forms
- `GET /api/forms/:formId` - Get single form (public)
- `PUT /api/forms/:formId` - Update form
- `DELETE /api/forms/:formId` - Delete form

### Submissions
- `POST /api/submissions/:formId/submit` - Submit form response
- `GET /api/submissions/:formId/responses` - Get all responses (owner only)

### Webhooks
- `POST /api/webhooks/airtable` - Airtable webhook endpoint

## 🧠 Conditional Logic Engine

The pure function `shouldShowQuestion(rules, answersSoFar)` evaluates visibility:

```javascript
// Example: Show GitHub URL only if role is "Engineer"
{
  logic: "AND",
  conditions: [
    { questionKey: "role", operator: "equals", value: "Engineer" }
  ]
}
```

**Supported Operators:**
- `equals` - Exact match
- `notEquals` - Not equal
- `contains` - String/Array contains value

**Logic Combinators:**
- `AND` - All conditions must be true
- `OR` - At least one condition must be true

## 📂 Project Structure

```
mern-airtable-form-builder/
├── backend/
│   ├── models/          # MongoDB schemas
│   ├── routes/          # API routes
│   ├── utils/           # Helper functions
│   ├── middleware/      # Auth middleware
│   └── server.js        # Entry point
└── frontend/
    └── src/
        ├── components/  # React components
        ├── services/    # API client
        └── App.jsx      # Main app
```

## 🎯 Usage Flow

1. **Login with Airtable** → OAuth authentication
2. **Select Base & Table** → Choose data source
3. **Build Form** → Select fields, add labels, set required fields
4. **Add Conditional Logic** → Define show/hide rules
5. **Share Form Link** → `/form/:formId`
6. **Collect Responses** → Saved to Airtable + MongoDB
7. **View Analytics** → See all submissions

## 🔧 Development Notes

### Supported Airtable Field Types
✅ Single Line Text
✅ Long Text
✅ Single Select
✅ Multiple Selects
✅ Attachments

❌ Unsupported: Checkbox, Date, Formula, Number, etc.

### Webhook Configuration
To enable real-time sync, configure Airtable webhook:
1. Use [Airtable Webhooks API](https://airtable.com/developers/web/api/webhooks-overview)
2. Set notification URL: `http://your-domain.com/api/webhooks/airtable`
3. Webhook will update/mark deleted records in MongoDB

## 🚀 Deployment

### Backend (Render/Railway)
1. Push code to GitHub
2. Connect repository to Render/Railway
3. Set environment variables
4. Deploy!

### Frontend (Vercel/Netlify)
1. Connect GitHub repository
2. Set build command: `npm run build`
3. Set output directory: `dist`
4. Deploy!

### Production Checklist
- [ ] Update `AIRTABLE_REDIRECT_URI` to production URL
- [ ] Set `NODE_ENV=production`
- [ ] Use MongoDB Atlas for production database
- [ ] Enable CORS for production frontend URL
- [ ] Add rate limiting
- [ ] Set up SSL certificates

## 📝 License

MIT License - feel free to use this project for learning or portfolio!

## 👤 Author

**Samarth Jain**
- GitHub: [@Samarth-27](https://github.com/Samarth-27)
- Portfolio: [Add your portfolio URL]

## 🙏 Acknowledgments

- Airtable API Documentation
- MERN Stack Community
- Built for interview/hackathon showcase

---

⭐ **Star this repo if you found it helpful!**
