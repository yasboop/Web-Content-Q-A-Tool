# Web Content Q&A Tool

A web application that allows users to ingest content from multiple URLs and ask questions about that content. The application uses Next.js for the frontend, FastAPI for the backend, and Mistral AI for generating answers based only on the ingested content.

![AiSensy Content Intelligence](https://i.imgur.com/your-screenshot-link.png)

## Features

- **Multi-URL Content Ingestion**: Input one or multiple webpage URLs to analyze
- **Content-Based Q&A**: Questions are answered strictly using the ingested content
- **Concise, Accurate Answers**: Powered by Mistral AI's language model
- **Modern UI**: Clean, responsive interface built with Next.js and TailwindCSS
- **No Persistent Storage**: Content is stored in-memory for the session only
- **Dark/Light Theme**: Toggle between light and dark modes for comfortable viewing

## Tech Stack

- **Frontend**: Next.js with React, TailwindCSS for styling
- **Backend**: FastAPI (Python) with httpx for async HTTP requests
- **Content Extraction**: Beautiful Soup and Playwright for handling dynamic content
- **AI Integration**: Mistral AI API for content-based question answering
- **Development**: Unified development environment with concurrent frontend/backend servers

## Prerequisites

- Node.js (v14+)
- Python (v3.8+)
- Mistral AI API key (obtainable from [Mistral AI Platform](https://console.mistral.ai/))

## Installation

### Local Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/web-content-qa.git
   cd web-content-qa
   ```

2. Install frontend dependencies:
   ```bash
   npm install
   ```

3. Install backend dependencies:
   ```bash
   # Create and activate a virtual environment (recommended)
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate

   # Install dependencies
   pip install -r requirements.txt
   ```

4. Set up environment variables:
   - Copy `.env.example` to `.env`
   - Add your Mistral API key to the `.env` file:
     ```
     MISTRAL_API_KEY=your_api_key_here
     ```

5. Run the development server (frontend + backend):
   ```bash
   npm run dev:all
   ```

6. Open [http://localhost:3000](http://localhost:3000) in your browser

## Project Structure

```
web-content-qa/
├── api/                  # FastAPI backend
│   ├── index.py          # Main API with advanced content extraction
│   ├── simple_api.py     # Simplified API version
│   └── clean_api.py      # Clean implementation with Mistral integration
├── components/           # React components
├── pages/                # Next.js pages
│   ├── api/              # Next.js API routes (proxies to FastAPI)
│   ├── _app.js          
│   └── index.js          # Main application page
├── public/               # Static assets
├── styles/               # CSS files
├── utils/                # Utility functions
├── dev.js                # Combined dev server (Next.js + FastAPI)
├── next.config.js        # Next.js configuration
├── package.json          # Node dependencies
├── tailwind.config.js    # Tailwind CSS configuration
└── requirements.txt      # Python dependencies
```

## How It Works

1. **Content Ingestion**:
   - User enters one or more URLs
   - Backend extracts content using advanced techniques:
     - Standard HTTP requests with BeautifulSoup for basic sites
     - Playwright headless browser for JavaScript-heavy sites
     - Special handling for academic sites with paywalls

2. **Session Management**:
   - Each content extraction session gets a unique ID
   - Content is stored in-memory for the session duration
   - No persistent storage - data is lost on server restart

3. **Question Answering**:
   - User asks a question about the ingested content
   - Question + extracted content are sent to Mistral AI
   - AI generates an answer strictly based on provided content
   - Fallback mechanisms handle API failures gracefully

## Deployment

### Vercel Deployment

1. Push your code to GitHub
2. Connect your GitHub repository to Vercel
3. Configure the build settings:
   - Build Command: `npm run build`
   - Output Directory: `.next`
4. Add environment variables:
   - `MISTRAL_API_KEY`: Your Mistral AI API key

### Backend Deployment

For the backend API, you can:
1. Deploy to Vercel Serverless Functions
2. Deploy to a cloud provider like Railway, Render, or Heroku
3. Update the `next.config.js` file to point to your deployed API

## API Reference

### `/api/scrape` (POST)
Extracts content from provided URLs.

**Request Body**:
```json
{
  "urls": ["https://example.com", "https://example2.com"],
  "session_id": "optional-existing-session-id"
}
```

**Response**:
```json
{
  "session_id": "generated-or-provided-session-id",
  "extraction_warnings": ["urls-with-extraction-issues"]
}
```

### `/api/ask` (POST)
Answers questions based on previously extracted content.

**Request Body**:
```json
{
  "question": "What is mentioned about X?",
  "session_id": "your-session-id"
}
```

**Response**:
```json
{
  "answer": "Based on the extracted content, X is described as..."
}
```

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgements

- [Next.js](https://nextjs.org)
- [FastAPI](https://fastapi.tiangolo.com)
- [Mistral AI](https://mistral.ai)
- [TailwindCSS](https://tailwindcss.com)
- [Playwright](https://playwright.dev) 