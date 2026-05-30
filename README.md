# DiFa Virtual Assistant

A comprehensive AI-powered virtual assistant application built for DiFa (Facility Planning Information System) that provides intelligent support, document search, and automated ticket creation capabilities.

## 🚀 Overview

DiFa Virtual Assistant is a full-stack web application that combines Azure OpenAI services with a React frontend to deliver an intelligent conversational interface. The system helps users find information, request access to various services, and automatically create ServiceNow tickets based on user interactions.

### Key Features

- **🤖 AI-Powered Chat Interface**: Intelligent conversational AI using Azure OpenAI GPT models
- **🔍 Semantic Search**: Advanced document search with Azure Cognitive Search
- **🎫 Automated Ticket Creation**: Direct integration with ServiceNow for incident management
- **🌐 Multi-language Support**: English and German language support with i18next
- **📁 File Upload & Processing**: Support for image and document analysis
- **📊 Analytics Integration**: Matomo tracking for user behavior analysis
- **🔐 Enterprise Authentication**: OAuth integration with secure session management
- **💾 Conversation History**: Persistent chat history with Azure Cosmos DB
- **📱 Responsive Design**: Modern UI with Fluent UI and Material-UI components

## 🏗️ Architecture

### Frontend (React + TypeScript)
- **Framework**: React 18 with TypeScript
- **Build Tool**: Vite
- **UI Libraries**: Fluent UI, Material-UI, Mercedes-Benz UI Components
- **State Management**: React Context API with custom reducers
- **Routing**: React Router DOM
- **Internationalization**: i18next for multi-language support

### Backend (Python Flask)
- **Framework**: Flask with async support
- **AI Services**: Azure OpenAI (GPT models, embeddings)
- **Search**: Azure Cognitive Search with semantic capabilities
- **Database**: Azure Cosmos DB for conversation storage
- **Authentication**: OAuth with JWT tokens and AES encryption
- **File Storage**: Azure Blob Storage
- **External Integration**: ServiceNow API for ticket creation

### Infrastructure
- **Hosting**: Azure App Service (Linux containers)
- **Monitoring**: Application Insights
- **Deployment**: ARM templates for infrastructure as code

## 📋 Prerequisites

- **Node.js** 18+ and npm
- **Python** 3.8+
- **Azure Subscription** with the following services:
  - Azure OpenAI Service
  - Azure Cognitive Search
  - Azure Cosmos DB
  - Azure Blob Storage
  - Azure App Service
  - Application Insights

## 🛠️ Installation & Setup

### 1. Clone the Repository
```bash
git clone <repository-url>
cd DiFa-virtualassistant
```

### 2. Backend Setup
```bash
# Install Python dependencies
pip install -r requirements.txt

# Set up environment variables (see Configuration section)
cp .env.example .env
# Edit .env with your Azure service credentials
```

### 3. Frontend Setup
```bash
cd frontend
npm install
```

### 4. Environment Configuration
Create a `.env` file in the root directory with the following variables:

```env
# Azure OpenAI Configuration
AZURE_OPENAI_ENDPOINT=your_openai_endpoint
AZURE_OPENAI_KEY=your_openai_key
AZURE_OPENAI_MODEL=your_model_deployment_name
AZURE_OPENAI_API_VERSION=2023-12-01-preview
AZURE_OPENAI_EMBEDDING_NAME=your_embedding_deployment

# Azure Search Configuration
AZURE_AI_SEARCH_ENDPOINT=your_search_endpoint
AZURE_SEARCH_KEY=your_search_key
AZURE_SEARCH_INDEX=your_search_index
AZURE_SEARCH_SEMANTIC_SEARCH_CONFIG=default

# Azure Cosmos DB Configuration
AZURE_COSMOSDB_ACCOUNT_ENDPOINT=your_cosmosdb_endpoint
AZURE_COSMOSDB_ACCOUNT_KEY=your_cosmosdb_key
AZURE_COSMOSDB_DATABASE=your_database_name
AZURE_COSMOSDB_CONVERSATIONS_CONTAINER=conversations

# Azure Blob Storage
AZURE_STORAGE_ACCOUNT_CONNECTION_STRING=your_storage_connection_string
ADLS_CONTAINER_NAME_CHAT_IMAGESTORE=your_container_name

# ServiceNow Integration
SNOW_API_URL=your_servicenow_api_url
SNOW_API_USERNAME=your_servicenow_username
SNOW_API_PASSWORD=your_servicenow_password

# Authentication
AUTH_CLIENT_ID=your_oauth_client_id
AUTH_CLIENT_SECRET=your_oauth_client_secret
ALICE_TOKEN_URL=your_token_endpoint
ALICE_AUTHORIZE_URL=your_authorize_endpoint
ALICE_USER_INFO_URL=your_userinfo_endpoint

# Application Settings
DEBUG_LOGGING=false
LOCAL_TESTING=false
ENCRYPTION_KEY=your_32_character_encryption_key
STRONG_SECRET_KEY=your_jwt_secret_key
```

## 🚀 Running the Application

### Development Mode

#### Backend
```bash
# Run Flask development server
python app.py
```
The backend starts with one of these modes:

- `LOCAL_TESTING=false`: `http://localhost:5000`
- `LOCAL_TESTING=true`: `https://127.0.0.1:8100`

For `LOCAL_TESTING=true`, place `cert.pem` and `key.pem` in the project root.

PowerShell + OpenSSL example:

```bash
openssl req -x509 -newkey rsa:4096 -sha256 -nodes -keyout key.pem -out cert.pem -days 365 -subj "/CN=localhost" -addext "subjectAltName=DNS:localhost,IP:127.0.0.1"
```

#### Frontend
```bash
cd frontend
npm run dev
```
The frontend will start on `http://localhost:5173`

### Production Build

#### Frontend Build
```bash
cd frontend
npm run build
```

#### Production Deployment
```bash
# The built frontend files are served by the Flask backend
python app.py
```

## 📁 Project Structure

```
DiFa-virtualassistant/
├── frontend/                          # React frontend application
│   ├── src/
│   │   ├── components/                # Reusable UI components
│   │   │   ├── Answer/               # Chat response components
│   │   │   ├── ChatHistory/          # Conversation history
│   │   │   ├── QuestionInput/        # User input interface
│   │   │   ├── FileUpload/           # File upload functionality
│   │   │   ├── PDFViewer/            # Document viewer
│   │   │   └── ...
│   │   ├── pages/                    # Application pages
│   │   ├── state/                    # State management
│   │   ├── api/                      # API client functions
│   │   ├── assets/                   # Static assets and localization
│   │   └── ...
│   ├── package.json
│   └── vite.config.ts
├── backend/                           # Python Flask backend
│   ├── auth/                         # Authentication utilities
│   ├── history/                      # Conversation history management
│   ├── automation/                   # Test automation
│   ├── utility.py                    # Core business logic
│   ├── keywords.py                   # Category classification
│   └── env_loader.py                 # Environment configuration
├── infrastructure/                    # Azure deployment templates
│   └── deployment.json               # ARM template
├── static/                           # Built frontend assets
├── Evaluations/                      # AI model evaluation tools
├── app.py                            # Main Flask application
├── requirements.txt                  # Python dependencies
└── README.md
```

## 🔧 Key Components

### Frontend Components

- **Chat Interface**: Real-time conversation with streaming responses
- **File Upload**: Support for images and documents with preview
- **Citation Display**: Source references for AI responses
- **Ticket Creation**: Forms for ServiceNow ticket generation
- **User Selection Dialog**: Multi-user request handling
- **Language Switcher**: Dynamic language switching

### Backend Services

- **ConversationDriver**: Core AI conversation logic
- **CosmosConversationClient**: Database operations for chat history
- **Authentication**: OAuth flow with token management
- **File Processing**: Image analysis and document handling
- **Search Integration**: Azure Cognitive Search queries
- **Ticket Management**: ServiceNow API integration

## 🌐 API Endpoints

### Chat & Conversation
- `POST /history/generate` - Generate AI responses
- `POST /history/update` - Update conversation history
- `GET /history/list` - List user conversations
- `POST /history/read` - Get conversation details
- `DELETE /history/delete` - Delete conversations

### Ticket Management
- `POST /history/snow_ticket` - Create ServiceNow tickets
- `POST /history/snow_descriptions_review` - Generate ticket descriptions

### User Management
- `GET /frontend_settings` - Get user settings and permissions
- `GET /api/check-access` - Verify user access rights
- `GET /api/check-poweruser-access` - Check power user permissions

### File Operations
- `POST /download` - Download files from blob storage

## 🔐 Security Features

- **OAuth Authentication**: Secure user authentication flow
- **JWT Tokens**: Encrypted token storage with automatic refresh
- **AES Encryption**: Sensitive data encryption
- **CSRF Protection**: Cross-site request forgery prevention
- **Security Headers**: Comprehensive HTTP security headers
- **Access Control**: Role-based permissions system

## 🌍 Internationalization

The application supports multiple languages:
- **English** (en)
- **German** (de)

Language files are located in `frontend/src/assets/locale/`

## 📊 Monitoring & Analytics

- **Application Insights**: Performance and error monitoring
- **Matomo Analytics**: User behavior tracking
- **Conversation Logging**: Chat history for analysis
- **Error Handling**: Comprehensive error logging and reporting

## 🧪 Testing

### Frontend Testing
```bash
cd frontend
npm test
```

### Backend Testing
```bash
python -m pytest backend/automation/testcases.py
```

## 🚀 Deployment

### Azure Deployment
1. Use the ARM template in `infrastructure/deployment.json`
2. Configure the required Azure services
3. Set environment variables in App Service configuration
4. Deploy using Azure CLI or Azure Portal

### Docker Deployment
The application can be containerized using the provided configuration for Azure Container Registry.

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📝 License

This project is proprietary software developed for DiFa. All rights reserved.

## 🆘 Support

For support and questions:
- Check the documentation in the `/docs` folder
- Review the FAQ section in the application
- Contact the development team

## 🔄 Version History

- **v1.0.0** - Initial release with core chat functionality
- **v1.1.0** - Added ServiceNow integration
- **v1.2.0** - Multi-language support
- **v1.3.0** - File upload and processing
- **v1.4.0** - Enhanced authentication and security

---

**Built with ❤️ for DiFa by the Development Team**
