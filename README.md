# LinkedIn Post Generator

AI-powered multi-agent system that generates engaging LinkedIn posts in different writing styles with professional images and performance tracking.

## Features

- **Multi-Agent AI System**: 5 different writing styles (Professional, Bold, Friendly, Expert, Concise)
- **Content Filtering**: Automatic quality and safety filtering
- **Image Generation**: Professional images using AI
- **Performance Tracking**: Token usage and cost estimation
- **One-Click Copy**: Easy copy-paste functionality
- **Real-time Generation**: Concurrent processing for speed
- **Health Monitoring**: Built-in health check endpoints
- **Deployment Ready**: Docker, cloud platforms, and local development support

### Local Development

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/linkedin-post-generator.git
   cd linkedin-post-generator
   ```

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Set up environment variables**
   ```bash
   cp .env.example .env
   # Edit .env and add your OPENROUTER_API_KEY
   ```

4. **Run the application**
   ```bash
   python app.py
   ```

5. **Open your browser**
   - Application: http://localhost:7860
   - Health check: http://localhost:8080/health
   - Metrics: http://localhost:8080/metrics

### Docker Deployment

```bash
# Using Docker Compose (recommended)
docker-compose up --build

# Or build manually
docker build -t linkedin-generator .
docker run -p 7860:7860 -p 8080:8080 --env-file .env linkedin-generator
```

## API Key Setup

### Getting Your OpenRouter API Key

1. Visit [OpenRouter.ai](https://openrouter.ai/)
2. Create a free account
3. Navigate to API Keys section
4. Generate a new API key
5. Copy the key (starts with `sk-or-...`)

### Configuration

Create a `.env` file in the project root:

```env
OPENROUTER_API_KEY=sk-or-your-actual-key-here
PORT=7860
HEALTH_PORT=8080
```

**Important**: Never commit your API key to version control. The `.gitignore` file is configured to exclude `.env` files.


## Usage Guide

### Basic Usage

1. **Enter Topic**: Describe what you want to post about
   - Example: "The future of remote work and its impact on company culture"
   - Example: "5 leadership lessons I learned from failure"

2. **Configure Preferences**:
   - **Tone**: Professional, casual, inspirational, educational, conversational, authoritative
   - **Length**: Short (~100 words), Medium (~200 words), Long (~300 words)
   - **Audience**: Target audience description (e.g., "startup founders", "marketing professionals")

3. **Optional Settings**:
   - **Hashtags**: Preferred hashtags to include
   - **Call-to-Action**: Type of engagement you want
   - **Number of Posts**: 3-5 posts with different styles

4. **Generate & Copy**: Click generate button, review posts, and copy your favorites

### Writing Styles Explained

- **Professional**: Formal, authoritative tone with industry insights
- **Bold**: Confident, opinion-driven posts that challenge conventional thinking
- **Friendly**: Warm, conversational tone that builds personal connections
- **Expert**: Technical authority with thought leadership perspective
- **Concise**: Brief, punchy messages that get straight to the point

## Architecture

### System Components

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Gradio UI     │    │  Flask Health   │    │  OpenRouter     │
│   Frontend      │    │  Monitor        │    │  API            │
│   Port 7860     │    │  Port 8080      │    │                 │
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                       │                       │
         └───────────────────────┼───────────────────────┘
                                │
         ┌─────────────────────────────────────────────────┐
         │              Main Application                   │
         │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐ │
         │  │   Content   │  │   Multi     │  │   Image     │ │
         │  │   Filter    │  │   Agent     │  │ Generator   │ │
         │  │             │  │   System    │  │             │ │
         │  └─────────────┘  └─────────────┘  └─────────────┘ │
         └─────────────────────────────────────────────────┘
```

### Technology Stack

- **Frontend**: Gradio with custom CSS styling
- **Backend**: Async Python with aiohttp
- **AI Models**: 
  - Text: Claude-3-Haiku via OpenRouter
  - Images: FLUX-1-Schnell via OpenRouter
- **Monitoring**: Flask endpoints for health checks
- **Deployment**: Docker, cloud platforms

### Performance Specifications

- **Generation Time**: 2-5 seconds for 3 posts
- **Cost per Generation**: $0.001-0.003 USD
- **Concurrent Processing**: All posts generated simultaneously
- **Memory Usage**: ~200-400MB
- **CPU Usage**: Single core sufficient
- **Concurrent Users**: 10-20 per instance (depends on hardware)

## API Reference

### Health Endpoints

#### Health Check
```http
GET /health
```

**Response**:
```json
{
  "status": "healthy",
  "service": "LinkedIn Post Generator",
  "version": "2.1",
  "timestamp": "2024-01-01T12:00:00Z",
  "features": [
    "Multi-agent AI generation",
    "Content filtering",
    "Image generation",
    "Professional formatting",
    "Copy functionality",
    "Performance tracking",
    "Cost estimation"
  ],
  "api_status": "connected"
}
```

#### Metrics
```http
GET /metrics
```

**Response**:
```json
{
  "uptime": "healthy",
  "api_key_configured": true,
  "agents_available": ["professional", "bold", "friendly", "expert", "concise"],
  "supported_models": ["anthropic/claude-3-haiku", "black-forest-labs/flux-1-schnell-free"]
}
```

## Configuration

### Environment Variables

| Variable | Required | Description | Default |
|----------|----------|-------------|---------|
| `OPENROUTER_API_KEY` | Yes | OpenRouter API key | None |
| `PORT` | No | Main application port | 7860 |
| `HEALTH_PORT` | No | Health check port | 8080 |
| `DEBUG` | No | Enable debug mode | false |
| `LOG_LEVEL` | No | Logging level | INFO |

