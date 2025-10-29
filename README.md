# 🎮 Broken.GG - League of Legends Match History Tracker

A full-stack web application inspired by OP.GG for tracking League of Legends summoner statistics and match history.

## 📋 Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Running with Docker](#running-with-docker)
- [Development Setup](#development-setup)
- [API Documentation](#api-documentation)
- [Contributing](#contributing)

## ✨ Features

- 🔍 Search summoners by name and tag (e.g., Faker#T1)
- 📊 View detailed match history with statistics
- 🏆 Display ranked information and mastery data
- 👥 Show all players in each match with champion details
- 📈 KDA, CS, Vision Score, and item tracking
- 🎯 Champion icons, summoner spells, and items display

## 🛠 Tech Stack

### Backend
- **.NET 9.0** - ASP.NET Core Web API
- **C#** - Programming language
- **Newtonsoft.Json** - JSON serialization
- **DotNetEnv** - Environment variable management
- **Swagger/OpenAPI** - API documentation

### Frontend
- **HTML5** - Structure
- **CSS3** - Styling
- **Vanilla JavaScript (ES6 Modules)** - Client-side logic
- **Nginx** - Static file serving (production)

### DevOps
- **Docker** - Containerization
- **Docker Compose** - Multi-container orchestration
- **GitHub Actions** - CI/CD (coming soon)

## 📁 Project Structure

```
BrokenGG/
├── Backend/                    # .NET API Server
│   ├── src/
│   │   ├── api/
│   │   │   ├── controller/    # API Controllers
│   │   │   ├── models/        # Data models
│   │   │   ├── service/       # Business logic & external APIs
│   │   │   └── .env          # Environment variables (not in git)
│   │   └── test/             # Unit tests
│   ├── Program.cs            # Application entry point
│   ├── Backend.csproj        # Project configuration
│   ├── Dockerfile            # Backend container config
│   └── README.md
│
├── Frontend/                  # Static Web Application
│   ├── public/
│   │   ├── index.html        # Home page
│   │   ├── src/
│   │   │   ├── js/           # JavaScript modules
│   │   │   ├── styles/       # CSS stylesheets
│   │   │   └── pages/        # Additional HTML pages
│   ├── Dockerfile            # Frontend container config
│   ├── nginx.conf            # Nginx configuration
│   └── README.md
│
├── docker-compose.yml        # Multi-service orchestration
└── README.md                 # This file
```

## 🚀 Getting Started

### Prerequisites

- **Docker** and **Docker Compose** (recommended)
  - OR -
- **.NET 9 SDK** for backend
- **Node.js** (optional, for frontend development)
- **Riot Games API Key** - Get one from [developer.riotgames.com](https://developer.riotgames.com/)

### Quick Start with Docker (Recommended)

1. **Clone the repository**
   ```bash
   git clone https://github.com/Broken-GG/Backend.git
   cd BrokenGG
   ```

2. **Set up environment variables**
   ```bash
   # Copy the example env file
   cp Backend/src/.env.example Backend/src/.env
   
   # Edit the .env file and add your Riot API key
   notepad Backend/src/.env  # Windows
   # or
   nano Backend/src/.env     # Linux/Mac
   ```

3. **Build and run with Docker Compose**
   ```bash
   docker-compose up --build
   ```

4. **Access the application**
   - Frontend: http://localhost
   - Backend API: http://localhost:5000
   - Swagger UI: http://localhost:5000/swagger

### 🔧 Development Setup (Without Docker)

#### Backend Setup

```bash
cd Backend

# Copy environment file
cp src/.env.example src/.env

# Edit src/.env and add your RIOT_API_KEY

# Restore dependencies
dotnet restore

# Run the backend
dotnet run
```

The API will be available at `http://localhost:5000`

#### Frontend Setup

```bash
cd Frontend

# Serve with Python (simple option)
python server.py

# OR use any static server
# Python 3
python -m http.server 8000 --directory public

# Node.js (npx)
npx serve public

# PHP
php -S localhost:8000 -t public
```

The frontend will be available at `http://localhost:8000`

## 🐳 Running with Docker

### Build and Run

```bash
# Build images
docker-compose build

# Start services
docker-compose up

# Run in background
docker-compose up -d

# View logs
docker-compose logs -f

# Stop services
docker-compose down
```

### Individual Services

```bash
# Build backend only
docker build -t brokengg-backend ./Backend

# Run backend
docker run -p 5000:5000 --env-file ./Backend/src/.env brokengg-backend

# Build frontend only
docker build -t brokengg-frontend ./Frontend

# Run frontend
docker run -p 80:80 brokengg-frontend
```

## 📚 API Documentation

### Base URL
- Development: `http://localhost:5000/api`
- Production: Configure in your deployment

### Endpoints

#### Get Summoner Info
```http
GET /api/SummonerInfo/{summonerName}/{tagLine}
```

**Example:**
```bash
curl http://localhost:5000/api/SummonerInfo/Faker/T1
```

**Response:**
```json
{
  "summonerName": "Faker",
  "tagline": "T1",
  "puuid": "...",
  "level": 623,
  "region": "EU",
  "profileIconUrl": "https://..."
}
```

#### Get Match History
```http
GET /api/MatchInfo/{puuid}?start=0&count=10
```

#### Get Match History by Summoner
```http
GET /api/MatchInfo/summoner/{summonerName}/{tagLine}?start=0&count=10
```

#### Get Ranked Info
```http
GET /api/SidePanelInfo/ranked/{puuid}
```

#### Get Mastery Info
```http
GET /api/SidePanelInfo/mastery/{puuid}
```

For full API documentation, visit `/swagger` when running the backend.

## 🧪 Testing

```bash
cd Backend
dotnet test
```

## 📦 Package Management

### Backend Dependencies
- Microsoft.AspNetCore.OpenApi (9.0.0)
- Swashbuckle.AspNetCore (6.8.1)
- Newtonsoft.Json (13.0.3)
- DotNetEnv (3.0.0)
- xUnit (2.9.2) - Testing
- Moq (4.20.72) - Mocking

### Frontend
- No build dependencies (vanilla JavaScript)
- Uses CDN for any external libraries

## 🔐 Environment Variables

| Variable | Description | Required |
|----------|-------------|----------|
| `RIOT_API_KEY` | Your Riot Games API key | Yes |
| `RIOT_API_URL` | Riot Account API endpoint | No (has default) |
| `RIOT_SUMMONER_URL` | Riot Summoner API endpoint | No (has default) |
| `ASPNETCORE_ENVIRONMENT` | Development/Production | No |

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is for educational purposes. League of Legends and all related properties are trademarks of Riot Games.

## 🐛 Known Issues

- Riot API key needs to be refreshed every 24 hours for development keys
- Some champion icons might not load if Data Dragon version changes

## 📞 Support

For issues and questions:
- Open an issue on GitHub
- Check existing issues for solutions

## 🎯 Roadmap

- [ ] Add caching layer (Redis)
- [ ] Implement CI/CD pipeline
- [ ] Add user authentication
- [ ] Store historical data in database
- [ ] Add more statistics and graphs
- [ ] Mobile responsive design improvements
- [ ] Add live game tracking

---

Made with ❤️ for the League of Legends community
