# 🚀 SocialPulse

**SocialPulse** is a full‑stack social engagement platform built with **.NET 8**, **React 18**, **SQL Server**, and **Redis**. This guide helps you get started with development, testing, and production deployment.

---

## 📋 Prerequisites

### 🔧 Software

- [.NET 8 SDK](https://dotnet.microsoft.com/download)
- [Node.js 18+](https://nodejs.org/)
- [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- [Git](https://git-scm.com/)
- IDE: **Visual Studio 2022** or **VS Code**

### 💾 Database & Caching

- **SQL Server** (LocalDB is sufficient for development)
- **Redis** (runs via Docker)

---

## 🛠️ Project Setup

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/SocialPulse.git
cd SocialPulse
```

### 2. Backend Setup (.NET API)

```bash
cd src/SocialPulse.API

dotnet restore            # Restore NuGet packages
dotnet ef database update # Apply EF Core migrations
dotnet run                # Run the API
```

> 📍 API available at: [https://localhost:7001](https://localhost:7001)

### 3. Frontend Setup (React)

```bash
cd src/SocialPulse.Client

npm install  # Install dependencies
npm start    # Start development server
```

> 📍 Frontend available at: [http://localhost:3000](http://localhost:3000)

### 4. Docker (Optional All-in-One Start)

```bash
docker-compose up -d          # Start all services
docker-compose logs -f        # View logs
```

---

## 🔧 Configuration

### `appsettings.Development.json`

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=(localdb)\\\\mssqllocaldb;Database=SocialPulseDB;Trusted_Connection=true;",
    "Redis": "localhost:6379"
  },
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  "AllowedHosts": "*"
}
```

### `.env`

```env
# Database
DATABASE_URL=Server=(localdb)\\mssqllocaldb;Database=SocialPulseDB;Trusted_Connection=true;
REDIS_URL=localhost:6379

# API Keys
SOCIAL_MEDIA_API_KEY=your_api_key_here
EMAIL_SERVICE_KEY=your_email_key_here

# JWT
JWT_SECRET=your_super_secret_jwt_key_here
JWT_ISSUER=SocialPulse
JWT_AUDIENCE=SocialPulse-Users
```

---

## 🐳 Docker Quick Start

| Task                                | Command                                                     |
| ----------------------------------- | ----------------------------------------------------------- |
| Infrastructure only (SQL + Redis)   | `docker-compose -f docker-compose.infrastructure.yml up -d` |
| Full stack (API + Redis + SQL + UI) | `docker-compose up -d`                                      |

---

## 🧪 Running Tests

### Unit Tests

```bash
cd tests/SocialPulse.Tests
dotnet test
```

### Integration Tests

```bash
cd tests/SocialPulse.IntegrationTests
dotnet test
```

### Code Coverage

```bash
dotnet test --collect:"XPlat Code Coverage"
```

---

## 📊 First Run Verification

| Service     | URL                                                                                    |
| ----------- | -------------------------------------------------------------------------------------- |
| API Swagger | [https://localhost:7001/swagger](https://localhost:7001/swagger)                       |
| React App   | [http://localhost:3000](http://localhost:3000)                                         |
| SignalR Hub | [https://localhost:7001/hubs/notifications](https://localhost:7001/hubs/notifications) |

### Example API Calls

```bash
# Health Check
curl https://localhost:7001/health

# Get Posts
curl https://localhost:7001/api/posts

# Create User
curl -X POST https://localhost:7001/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{"username":"testuser","email":"test@example.com","password":"Test123!"}'
```

---

## 🚀 Production Deployment

### GitHub Actions CI/CD

```bash
git checkout -b feature/new-feature
# Make changes
git commit -m "Add new feature"
git push origin feature/new-feature
```

### Docker Production Image

```bash
docker build -t socialpulse:prod .
docker run -d -p 80:80 socialpulse:prod
```

---

## 🔍 Troubleshooting

| Issue                     | Solution                                                                         |
| ------------------------- | -------------------------------------------------------------------------------- |
| Database connection error | `dotnet ef database drop && dotnet ef database update`                           |
| Redis connection error    | `docker run -d -p 6379:6379 redis:alpine`                                        |
| Port conflict             | Change ports in `launchSettings.json` or use `PORT=3001 npm start` for frontend. |
| SSL certificate error     | `dotnet dev-certs https --trust`                                                 |

---

## 📄 License

Distributed under the MIT License. See `LICENSE` for details.
