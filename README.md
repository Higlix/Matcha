# Web Matcha 💕

> A modern, full-stack dating application built with Go, React, and PostgreSQL

## 🎯 Project Objective

Web Matcha is a comprehensive dating platform that facilitates connections between users through an intelligent matching system. The application covers the entire dating journey from registration to real-time messaging, featuring GPS-based proximity matching, advanced search capabilities, and a sophisticated user rating system.

### Key Features
- 🔐 **Secure Authentication** - Email verification, JWT tokens, password reset
- 📍 **GPS Location Matching** - Find potential matches in your neighborhood
- 💬 **Real-time Chat** - Instant messaging between matched users
- 🔔 **Live Notifications** - Real-time updates for likes, matches, and messages
- ⭐ **Fame Rating System** - Dynamic user popularity scoring
- 🔍 **Advanced Search** - Multi-criteria filtering and sorting
- 📱 **Mobile Responsive** - Optimized for all devices
- 🛡️ **Privacy & Security** - Comprehensive protection against common vulnerabilities

## 🛠️ Tech Stack

### Backend
- **Framework**: [Gin](https://gin-gonic.com/) (Go HTTP web framework)
- **Database**: [PostgreSQL](https://www.postgresql.org/) with [PostGIS](https://postgis.net/) extension
- **Database Driver**: [pgx](https://github.com/jackc/pgx) (Pure Go PostgreSQL driver)
- **Authentication**: [golang-jwt](https://github.com/golang-jwt/jwt) with bcrypt password hashing
- **Real-time**: [Gorilla WebSocket](https://github.com/gorilla/websocket)
- **Email**: [SendGrid](https://sendgrid.com/) integration
- **File Upload**: Native Go with image validation
- **Migrations**: [golang-migrate](https://github.com/golang-migrate/migrate)

### Frontend
- **Framework**: [React 18](https://reactjs.org/) with [TypeScript](https://www.typescriptlang.org/)
- **HTTP Client**: [Axios](https://axios-http.com/)
- **Real-time**: WebSocket client for live features
- **Routing**: [React Router](https://reactrouter.com/)
- **Styling**: CSS3 with responsive design

### Infrastructure
- **Containerization**: Docker & Docker Compose
- **Reverse Proxy**: Nginx
- **SSL/TLS**: Let's Encrypt certificates
- **File Storage**: Local filesystem with CDN capability
- **Monitoring**: Prometheus & Grafana ready

### Development Tools
- **Environment**: [godotenv](https://github.com/joho/godotenv) for configuration
- **Testing**: Go's built-in testing + [testify](https://github.com/stretchr/testify)
- **Code Quality**: golangci-lint, prettier for TypeScript
- **API Documentation**: Swagger/OpenAPI ready

## 🚀 Getting Started

### Prerequisites
- Go 1.21+
- Node.js 18+
- PostgreSQL 14+ with PostGIS extension
- Docker & Docker Compose (optional)

### Local Development Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/web-matcha.git
   cd web-matcha
   ```

2. **Set up environment variables**
   ```bash
   cp .env.example .env
   # Edit .env with your configuration
   ```

3. **Start PostgreSQL with PostGIS**
   ```bash
   docker run --name dating-db -e POSTGRES_PASSWORD=yourpassword -p 5432:5432 -d postgis/postgis
   ```

4. **Run database migrations**
   ```bash
   migrate -path migrations -database "postgres://username:password@localhost/dating_app?sslmode=disable" up
   ```

5. **Install backend dependencies**
   ```bash
   go mod download
   ```

6. **Install frontend dependencies**
   ```bash
   cd frontend
   npm install
   ```

7. **Start the development servers**
   ```bash
   # Terminal 1 - Backend
   go run cmd/main.go
   
   # Terminal 2 - Frontend
   cd frontend && npm start
   ```

8. **Access the application**
   - Frontend: http://localhost:3000
   - Backend API: http://localhost:8080/api

### Docker Setup (Alternative)
```bash
docker-compose up -d
```

## 📊 Database Schema

The application uses PostgreSQL with PostGIS for efficient geographic queries:

- **users** - Authentication and account data
- **profiles** - User profile information with location
- **photos** - Image uploads (max 5 per user)
- **likes** - User preferences and mutual matching
- **matches** - Connected users who can chat
- **messages** - Real-time chat conversations
- **profile_views** - Visit tracking for fame rating
- **blocked_users** - User blocking functionality
- **reports** - Fake account reporting system

## 🔧 API Endpoints

### Authentication
- `POST /api/register` - User registration
- `POST /api/login` - User authentication
- `GET /api/verify-email` - Email verification
- `POST /api/reset-password` - Password reset

### Profile Management
- `GET /api/profile` - Get user profile
- `PUT /api/profile` - Update profile
- `POST /api/upload` - Photo upload
- `DELETE /api/photos/:id` - Delete photo

### Matching & Search
- `GET /api/browse` - Get suggested matches
- `POST /api/search` - Advanced search
- `POST /api/like/:id` - Like a user
- `DELETE /api/like/:id` - Unlike a user
- `GET /api/matches` - Get user matches

### Chat & Notifications
- `WS /ws` - WebSocket connection for real-time features
- `GET /api/messages/:matchId` - Get chat history
- `GET /api/notifications` - Get notifications

## 🔒 Security Features

- **Password Security**: bcrypt hashing with cost factor 12
- **JWT Authentication**: Short-lived access tokens with refresh mechanism
- **SQL Injection Prevention**: Parameterized queries exclusively
- **XSS Protection**: Input sanitization and validation
- **File Upload Security**: Type validation, size limits, secure storage
- **Rate Limiting**: API endpoint protection
- **CORS Configuration**: Secure cross-origin requests

## 📱 Real-time Features

Web Matcha provides instant updates through WebSocket connections:

- **Live Chat**: Messages delivered within 3 seconds
- **Match Notifications**: Instant alerts when mutual likes occur
- **Online Status**: Real-time user presence indicators
- **Typing Indicators**: Live chat feedback
- **Push Notifications**: Offline message delivery

## 🌍 Location Features

Advanced geospatial capabilities powered by PostGIS:

- **GPS Integration**: Automatic location detection
- **Privacy Controls**: Neighborhood-level precision
- **Distance Calculation**: Efficient proximity matching
- **Location Search**: Geographic filtering and sorting
- **Manual Override**: User-controlled location adjustment

## 📈 Performance

Designed to handle 500+ concurrent users:

- **Database Optimization**: GiST indexes for location queries
- **Connection Pooling**: Efficient database connections
- **Image Optimization**: Automatic compression and resizing
- **Caching Strategy**: Redis integration ready
- **Load Balancing**: Nginx reverse proxy support

## 🧪 Testing

```bash
# Run backend tests
go test ./...

# Run frontend tests
cd frontend && npm test

# Run integration tests
go test -tags=integration ./...
```

## 🚀 Deployment

### Production Build
```bash
# Build frontend
cd frontend && npm run build

# Build backend
CGO_ENABLED=0 GOOS=linux go build -o main cmd/main.go

# Docker build
docker build -t web-matcha .
```

### Environment Variables
Key configuration variables for production:
- `DB_HOST`, `DB_PASSWORD` - Database connection
- `JWT_SECRET` - Token signing key
- `SENDGRID_API_KEY` - Email service
- `UPLOAD_PATH` - File storage location

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Built as part of a web development curriculum
- Inspired by modern dating applications
- Uses open-source technologies and best practices

---

**Note**: This is an educational project showcasing full-stack development skills with modern technologies. All features are implemented with security and scalability in mind.