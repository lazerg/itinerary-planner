# 🌍 AI Travel Itinerary Planner

An intelligent travel itinerary planning application powered by OpenAI's GPT-4o-mini, built with Vue 3, TypeScript, and Bulma CSS framework.

## 📋 Project Information

This application helps travelers create personalized travel itineraries using artificial intelligence. Users can input their travel preferences including destination, duration, group size, traveler type, and preferred language, and receive a comprehensive itinerary with detailed information about places to visit, historical context, travel tips, and practical advice.

### ✨ Key Features

- **AI-Powered Itinerary Generation**: Leverages OpenAI GPT-4o-mini for intelligent travel planning
- **Multi-Language Support**: Generate itineraries in English, Russian, and Uzbek
- **PDF Export**: Export generated itineraries as professional PDF documents
- **Responsive Design**: Beautiful, airport-themed interface with animated elements
- **Real-time Generation**: Live feedback during itinerary creation process
- **Clean Output**: Simple, readable text format optimized for clarity

### 🛠 Tech Stack

- **Frontend**: Vue 3 with Composition API
- **Language**: TypeScript
- **Styling**: Bulma CSS Framework + Custom CSS
- **Icons**: Font Awesome
- **PDF Generation**: jsPDF + html2canvas
- **AI Integration**: OpenAI GPT-4o-mini API
- **Build Tool**: Vite
- **Package Manager**: Yarn

## 🚀 Project Setup

### Prerequisites

- Node.js (v16 or higher)
- Yarn package manager
- OpenAI API key

### Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd itinerary-planner
   ```

2. **Install dependencies**
   ```bash
   yarn install
   ```

3. **Environment Setup**
   
   Create a `.env` file in the root directory:
   ```bash
   cp .env.example .env
   ```
   
   Add your OpenAI API key to the `.env` file:
   ```
   VITE_OPENAI_API_KEY=your-openai-api-key-here
   ```
   
   **⚠️ Important**: You must obtain an OpenAI API key from [OpenAI Platform](https://platform.openai.com/api-keys) and add it to your `.env` file for the application to work.

### 🏃‍♂️ Development

**Start the development server**
```bash
yarn dev
```

The application will be available at `http://localhost:5173`

### 🏗 Build for Production

**Create production build**
```bash
yarn build
```

**Preview production build**
```bash
yarn preview
```

### 🚀 Deploy and Publish

#### **Automatic GitHub Pages Deployment (Recommended)**

This project includes a GitHub Actions workflow that automatically builds and deploys to GitHub Pages on every push to the main branch.

**Setup Steps:**
1. **Enable GitHub Pages in your repository:**
   - Go to Settings → Pages
   - Source: "GitHub Actions"

2. **Add OpenAI API Key to GitHub Secrets:**
   - Go to Settings → Secrets and Variables → Actions
   - Add new repository secret: `VITE_OPENAI_API_KEY`
   - Set the value to your OpenAI API key

3. **Push to main branch:**
   ```bash
   git add .
   git commit -m "Setup GitHub Pages deployment"
   git push origin main
   ```

4. **Access your deployed app:**
   - Your app will be available at: `https://[username].github.io/itinerary-planner/`
   - Check the Actions tab to monitor deployment status

#### **Manual Deployment Options**

**For static hosting (Netlify, Vercel):**
1. Build the project: `yarn build`
2. Deploy the `dist` folder to your hosting service
3. Set environment variable: `VITE_OPENAI_API_KEY`

**For Docker deployment:**
```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN yarn install
COPY . .
RUN yarn build
EXPOSE 4173
CMD ["yarn", "preview", "--host"]
```

**Environment Variables in Production:**
- `VITE_OPENAI_API_KEY`: Your OpenAI API key (required for AI functionality)

## 🔄 CI/CD Pipeline

This project includes a robust GitHub Actions workflow that:

- **Automatic Building**: Builds the project on every push and pull request
- **Dependency Caching**: Uses Yarn cache for faster builds
- **Environment Security**: Safely handles API keys through GitHub Secrets
- **GitHub Pages Deployment**: Automatically deploys to GitHub Pages on main branch pushes
- **Build Optimization**: Creates optimized production bundles with code splitting

**Workflow Features:**
- ✅ Node.js 18 environment
- ✅ Yarn package manager
- ✅ Build artifact upload
- ✅ Automatic GitHub Pages deployment
- ✅ Concurrent deployment protection
- ✅ Manual workflow dispatch option

## 🎨 Features in Detail

### Language Support
- **English**: Full interface and content generation
- **Russian**: Interface labels and content in Russian
- **Uzbek**: Interface labels and content in Uzbek

### Form Inputs
- Leading tourist name
- Language preference
- Number of tourists (1-10)
- Tourist type (Family, Business, Adventure, etc.)
- Travel season
- Destination city
- Trip duration (1-15 days)

### Output Format
- General destination information
- Travel tips and important notes
- Day-by-day itinerary breakdown
- Detailed place information including:
  - Historical background
  - Transportation details
  - Practical tips
  - Special attractions

## 👨‍💻 Development Credits

This project was crafted with **Vibe Coding** - a development approach focused on creating engaging, user-friendly applications with attention to both functionality and aesthetic appeal.

## 🤝 Contributing

We welcome contributions to improve this project! 

### How to Contribute
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Open for Merge Requests
This project is **open for new merge requests**! Whether you want to:
- Add new languages
- Improve the UI/UX
- Enhance the AI prompts
- Add new features
- Fix bugs
- Improve documentation

We encourage developers to contribute and help make this tool even better.

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

## 🆘 Support

If you encounter any issues or have questions:
1. Check existing issues in the repository
2. Create a new issue with detailed information
3. Contact the development team

---

**Made with ❤️ by Vibe Coding | Powered by AI • FarkhodMaxTravel Group**