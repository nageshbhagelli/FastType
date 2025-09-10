# FastType ⚡

A modern, minimalistic typing test web application inspired by Monkeytype. Built with React, TypeScript, and Node.js.

## 🎯 Features

- **Real-time typing tests** with accurate WPM and accuracy tracking
- **Multiple test modes**: Time-based, word-based, quotes, and custom text
- **Extensive customization**: Themes, fonts, caret styles, and more
- **User accounts** with progress tracking and statistics
- **Performance analytics** with detailed charts and insights
- **Responsive design** optimized for all devices
- **Accessibility focused** with keyboard navigation and screen reader support

## 🚀 Quick Start

### Prerequisites
- Node.js 18+ LTS
- npm or yarn
- Git

### Development Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/fasttype.git
   cd fasttype
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Set up environment variables**
   ```bash
   cp .env.example .env
   # Edit .env with your configuration
   ```

4. **Start development servers**
   ```bash
   # Start frontend (React)
   npm run dev:frontend
   
   # Start backend (Node.js) - in another terminal
   npm run dev:backend
   ```

5. **Open your browser**
   - Frontend: http://localhost:3000
   - Backend API: http://localhost:5000

## 📁 Project Structure

```
fasttype/
├── frontend/          # React TypeScript frontend
├── backend/           # Node.js Express backend
├── shared/            # Shared types and utilities
├── docs/              # Documentation
├── scripts/           # Build and deployment scripts
└── tests/             # End-to-end tests
```

For detailed structure, see [PROJECT_STRUCTURE.md](PROJECT_STRUCTURE.md)

## 🛠️ Technology Stack

### Frontend
- **React 18+** with TypeScript
- **Vite** for fast development and building
- **Tailwind CSS** for styling
- **Zustand** for state management
- **Chart.js** for performance visualization

### Backend
- **Node.js** with Express.js
- **PostgreSQL** with Prisma ORM
- **JWT** for authentication
- **bcrypt** for password hashing

### DevOps
- **Docker** for containerization
- **Vercel** for frontend deployment
- **Railway** for backend deployment
- **GitHub Actions** for CI/CD

## 📚 Documentation

- [Product Requirements Document (PRD)](PRD.md)
- [Architecture Requirements Document (ARD)](ARD.md)
- [Project Structure](PROJECT_STRUCTURE.md)
- [API Documentation](docs/api/)
- [Deployment Guide](docs/deployment/)

## 🧪 Testing

```bash
# Run all tests
npm test

# Run frontend tests
npm run test:frontend

# Run backend tests
npm run test:backend

# Run E2E tests
npm run test:e2e
```

## 🚀 Deployment

### Development
```bash
docker-compose up -d
```

### Production
See [Deployment Guide](docs/deployment/production.md) for detailed instructions.

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

See [Contributing Guide](docs/development/contributing.md) for detailed guidelines.

## 📊 Performance Targets

- **Keystroke Latency**: <50ms
- **Page Load Time**: <2 seconds
- **Uptime**: 99.9%
- **Accuracy**: Precise WPM calculations
- **Accessibility**: WCAG 2.1 AA compliant

## 🎨 Customization

FastType offers extensive customization options:
- **Themes**: Dark, light, high contrast, and community themes
- **Fonts**: Multiple monospace font options
- **Caret**: Various styles and animations
- **Test Modes**: Time, words, quotes, custom text
- **Languages**: Multiple language support

## 📈 Roadmap

### Phase 1 (Weeks 1-2) - Foundation ✅
- [x] Basic typing test functionality
- [x] Real-time WPM and accuracy tracking
- [x] Core UI components

### Phase 2 (Weeks 3-4) - Enhanced Features
- [ ] Multiple test modes
- [ ] Statistics and performance charts
- [ ] Theme system and customization

### Phase 3 (Weeks 5-6) - User System
- [ ] User authentication
- [ ] Progress tracking
- [ ] Personal statistics dashboard

### Phase 4 (Weeks 7-8) - Advanced Features
- [ ] Leaderboards and achievements
- [ ] Command palette
- [ ] Social features

### Phase 5 (Weeks 9-10) - Polish & Launch
- [ ] Performance optimization
- [ ] Accessibility improvements
- [ ] Production deployment

## 🐛 Bug Reports & Feature Requests

Please use the [GitHub Issues](https://github.com/yourusername/fasttype/issues) page to report bugs or request features.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Inspired by [Monkeytype](https://monkeytype.com/)
- Built with modern web technologies
- Community feedback and contributions

## 📞 Support

- **Documentation**: Check our [docs](docs/) folder
- **Issues**: [GitHub Issues](https://github.com/yourusername/fasttype/issues)
- **Discussions**: [GitHub Discussions](https://github.com/yourusername/fasttype/discussions)

---

**Made with ❤️ for the typing community**
