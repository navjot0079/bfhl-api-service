# BFHL REST API

A production-ready REST API with mathematical operations and AI integration, built with Node.js and Express.

## 🚀 Features

- ✅ Strict API response structure
- ✅ Correct HTTP status codes
- ✅ Robust input validation
- ✅ Graceful error handling
- ✅ Security guardrails (Helmet, CORS, Rate Limiting)
- ✅ Google Gemini AI integration
- ✅ Comprehensive error messages
- ✅ Boundary condition handling

## 📡 API Endpoints

### 1. POST /bfhl

Main endpoint that handles five different operations based on the request key.

#### Operations

| Key | Input Type | Output | Description |
|-----|------------|--------|-------------|
| `fibonacci` | Integer | Array of integers | Generates Fibonacci sequence |
| `prime` | Integer array | Array of integers | Filters prime numbers |
| `lcm` | Integer array | Integer | Calculates LCM |
| `hcf` | Integer array | Integer | Calculates HCF/GCD |
| `AI` | String | String | AI-powered single-word answer |

#### Request Examples

**Fibonacci:**
```json
{
  "fibonacci": 7
}
```

**Prime:**
```json
{
  "prime": [2, 4, 7, 9, 11]
}
```

**LCM:**
```json
{
  "lcm": [12, 18, 24]
}
```

**HCF:**
```json
{
  "hcf": [24, 36, 60]
}
```

**AI:**
```json
{
  "AI": "What is the capital city of Maharashtra?"
}
```

#### Response Structure

**Success Response:**
```json
{
  "is_success": true,
  "official_email": "your.email@chitkara.edu.in",
  "data": <result>
}
```

**Error Response:**
```json
{
  "is_success": false,
  "official_email": "your.email@chitkara.edu.in",
  "error": "Error message"
}
```

### 2. GET /health

Health check endpoint to verify API status.

**Response:**
```json
{
  "is_success": true,
  "official_email": "your.email@chitkara.edu.in"
}
```

## 🛠️ Installation & Setup

### Prerequisites
- Node.js >= 18.0.0
- npm or yarn

### Local Development

1. **Clone the repository:**
```bash
git clone <your-repo-url>
cd Project
```

2. **Install dependencies:**
```bash
npm install
```

3. **Configure environment variables:**
```bash
# Copy the example env file
cp .env.example .env

# Edit .env and add:
# - Your Chitkara official email
# - Google Gemini API key (get from https://aistudio.google.com)
```

4. **Run the server:**
```bash
# Development mode (with auto-reload)
npm run dev

# Production mode
npm start
```

The API will be available at `http://localhost:3000`

## 🔑 Getting Google Gemini API Key

1. Visit [Google AI Studio](https://aistudio.google.com)
2. Sign in with your Google account
3. Click "Get API Key"
4. Create API key in new or existing project
5. Copy the key and add to `.env` file

## 🧪 Testing the API

### Using cURL

**Test Health Endpoint:**
```bash
curl http://localhost:3000/health
```

**Test Fibonacci:**
```bash
curl -X POST http://localhost:3000/bfhl \
  -H "Content-Type: application/json" \
  -d "{\"fibonacci\": 7}"
```

**Test Prime:**
```bash
curl -X POST http://localhost:3000/bfhl \
  -H "Content-Type: application/json" \
  -d "{\"prime\": [2, 4, 7, 9, 11]}"
```

**Test LCM:**
```bash
curl -X POST http://localhost:3000/bfhl \
  -H "Content-Type: application/json" \
  -d "{\"lcm\": [12, 18, 24]}"
```

**Test HCF:**
```bash
curl -X POST http://localhost:3000/bfhl \
  -H "Content-Type: application/json" \
  -d "{\"hcf\": [24, 36, 60]}"
```

**Test AI:**
```bash
curl -X POST http://localhost:3000/bfhl \
  -H "Content-Type: application/json" \
  -d "{\"AI\": \"What is the capital city of Maharashtra?\"}"
```

### Using Postman

1. Create a new POST request to `http://localhost:3000/bfhl`
2. Set header: `Content-Type: application/json`
3. Add JSON body with one of the operation keys
4. Send request

## 🚀 Deployment

### Vercel (Recommended)

1. Install Vercel CLI:
```bash
npm i -g vercel
```

2. Deploy:
```bash
vercel
```

3. Add environment variables in Vercel dashboard:
   - `OFFICIAL_EMAIL`
   - `GEMINI_API_KEY`

**Or deploy via GitHub:**
1. Login to [Vercel](https://vercel.com)
2. New Project → Import your GitHub repository
3. Configure environment variables
4. Deploy

### Railway

1. Login to [Railway](https://railway.app)
2. New Project → Deploy from GitHub
3. Select your repository
4. Add environment variables:
   - `OFFICIAL_EMAIL`
   - `GEMINI_API_KEY`
5. Deploy

### Render

1. Login to [Render](https://render.com)
2. New → Web Service
3. Connect your GitHub repository
4. Configure:
   - **Build Command:** `npm install`
   - **Start Command:** `npm start`
5. Add environment variables
6. Create Web Service

### ngrok (Testing Only)

```bash
# Install ngrok
npm i -g ngrok

# Start your local server
npm start

# In another terminal, expose it
ngrok http 3000
```

⚠️ **Note:** ngrok URLs expire and require your local server to remain running.

## 🔒 Security Features

- **Helmet.js**: Secures HTTP headers
- **CORS**: Cross-Origin Resource Sharing enabled
- **Rate Limiting**: 100 requests per 15 minutes per IP
- **Input Validation**: Comprehensive validation for all inputs
- **Error Handling**: Graceful error handling without crashes
- **Request Size Limiting**: 10MB max payload

## ✅ Validation Rules

### Fibonacci
- Must be a non-negative integer
- Maximum value: 1000

### Prime
- Must be an array of integers
- Array cannot be empty
- Maximum array size: 10000

### LCM / HCF
- Must be an array of non-zero integers
- Array cannot be empty
- Maximum array size: 1000

### AI
- Must be a non-empty string
- Maximum length: 1000 characters

## 📋 Error Codes

| Status Code | Description |
|-------------|-------------|
| 200 | Success |
| 400 | Bad Request (validation error) |
| 404 | Endpoint not found |
| 429 | Too many requests (rate limit) |
| 500 | Internal server error |

## 🧪 Test Cases Covered

- ✅ Exact match operations
- ✅ Boundary conditions (empty arrays, zero, negative numbers)
- ✅ Invalid input types
- ✅ Multiple keys in request
- ✅ Missing keys
- ✅ Invalid JSON format
- ✅ Security edge cases (SQL injection attempts, XSS)
- ✅ Rate limiting
- ✅ Large input arrays
- ✅ AI fallback when API key not configured

## 📦 Project Structure

```
Project/
├── server.js           # Main application file
├── package.json        # Dependencies and scripts
├── .env.example        # Environment variables template
├── .gitignore         # Git ignore rules
├── vercel.json        # Vercel deployment config
└── README.md          # Documentation
```

## 🛡️ Dependencies

- **express**: Web framework
- **dotenv**: Environment variable management
- **cors**: CORS middleware
- **helmet**: Security headers
- **express-rate-limit**: Rate limiting
- **axios**: HTTP client for AI API calls

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## 📄 License

MIT License

## 👨‍💻 Author

Chitkara University Student

## 🔗 Links

- **Repository:** [GitHub URL]
- **Live API:** [Deployment URL]
- **Health Check:** [Deployment URL]/health

---

**Note:** Make sure to replace placeholders in `.env` with your actual values before deploying!
