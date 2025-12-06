# Data Insights AI

**Professional Data Intelligence Platform powered by Manus AI**

A comprehensive, AI-driven data analysis platform that transforms raw CSV data into actionable insights through advanced statistical analysis, trend detection, anomaly identification, and intelligent data cleaning.

## Live Demo

**Deployed Application**: [https://datainsights-erft3lrq.manus.space](https://datainsights-erft3lrq.manus.space)

## Features

### 📊 Comprehensive Data Analysis
- **Advanced Statistical Analysis**: Calculate mean, median, standard deviation, quartiles, and more
- **Trend Detection**: Identify temporal patterns and trends in your data
- **Anomaly Detection**: Automatically detect outliers and unusual patterns
- **Data Quality Assessment**: Evaluate data completeness, consistency, and integrity

### 🧹 Intelligent Data Cleaning
- **AI-Powered Cleaning**: Automatically detect and fix data quality issues
- **Format Standardization**: Normalize data types and formats across columns
- **Missing Value Handling**: Intelligently handle missing or null values
- **Column Label Improvement**: Enhance column names and structure
- **Export Cleaned Data**: Download cleaned CSV files for further analysis

### 🤖 Multi-Faceted AI Insights
- **8 Analysis Categories**:
  - Overview & Structure
  - Statistical Analysis
  - Data Quality
  - Trends & Patterns
  - Anomalies & Outliers
  - Key Insights
  - Recommendations
  - Risk Assessment

- **Confidence Scoring**: Each insight includes a confidence score
- **Category Filtering**: Filter insights by analysis category
- **Detailed Reports**: Comprehensive analysis reports with actionable recommendations

### 💾 Data Management
- **CSV Upload**: Upload CSV files up to 10MB
- **Dataset Storage**: Store and manage multiple datasets
- **Recent Datasets**: Quick access to previously analyzed datasets
- **Data Preservation**: Maintain data integrity throughout the analysis process

## Technology Stack

### Frontend
- **React 19**: Modern UI framework with hooks and concurrent features
- **Tailwind CSS 4**: Utility-first CSS framework for responsive design
- **shadcn/ui**: High-quality, accessible React components
- **Lucide Icons**: Beautiful, consistent icon library
- **tRPC**: End-to-end type-safe API communication
- **Wouter**: Lightweight client-side routing

### Backend
- **Express 4**: Fast, minimalist web framework
- **tRPC 11**: Type-safe RPC framework
- **Drizzle ORM**: Lightweight, type-safe SQL query builder
- **MySQL/TiDB**: Relational database

### AI & Data Processing
- **Manus LLM API**: Advanced language model for data analysis
- **JSON Schema**: Structured response generation
- **simple-statistics**: Statistical computation library

### Infrastructure
- **Manus Platform**: Managed hosting and OAuth authentication
- **S3 Storage**: File storage and management
- **Node.js**: JavaScript runtime

## Architecture

### System Design

```
┌─────────────────────────────────────────────────────────────┐
│                    Frontend (React 19)                      │
│  ┌──────────────────────────────────────────────────────┐   │
│  │  Home Page (Upload & Analysis)                       │   │
│  │  - CSV Upload Dialog                                 │   │
│  │  - Recent Datasets List                  　           │ 　│
│  │  - Analysis Results View                　            │ 　│
│  │  - Data Cleaning Interface      　           　       │ 　│
│  └──────────────────────────────────────────────────────┘   │
└────────────────────────┬────────────────────────────────────┘
                         │ tRPC Calls
                         ▼
┌─────────────────────────────────────────────────────────────┐
│                   Backend (Express + tRPC)                  │
│  ┌──────────────────────────────────────────────────────┐ 　│
│  │  tRPC Routers                                        │　 │
│  │  ├─ csv.upload: Upload and parse CSV files         　│ 　 │
│  │  ├─ csv.list: Retrieve stored datasets            　　│ 　│
│  │  ├─ insights.generate: Generate AI insights       　　│ 　│
│  │  ├─ insights.list: Retrieve cached insights       　　│　 │
│  │  └─ cleaning.clean: AI-powered data cleaning      　　│　 │
│  └──────────────────────────────────────────────────────┘ 　│
└────────────────────────┬────────────────────────────────────┘
                         │
        ┌────────────────┼────────────────┐
        ▼                ▼                ▼
   ┌─────────┐    ┌────────────┐    ┌──────────┐
   │ Database│    │ Manus LLM  │    │ Storage  │
   │ (MySQL) │    │   API      │    │  (S3)    │
   └─────────┘    └────────────┘    └──────────┘
```

### Data Flow

1. **Upload Phase**
   - User uploads CSV file
   - File is parsed and validated
   - Data is stored in database
   - Dataset metadata is recorded

2. **Analysis Phase**
   - CSV content is sent to Manus LLM API
   - LLM performs multi-faceted analysis
   - Results are structured using JSON Schema
   - Insights are stored in database with confidence scores

3. **Cleaning Phase**
   - User initiates data cleaning
   - Manus LLM analyzes data quality issues
   - Cleaning recommendations are generated
   - Cleaned CSV is generated and made available for download

## Database Schema

### Tables

**users**
- `id`: Primary key
- `openId`: Manus OAuth identifier
- `name`: User name
- `email`: User email
- `role`: User role (user/admin)
- `createdAt`: Account creation timestamp
- `updatedAt`: Last update timestamp

**csvDatasets**
- `id`: Primary key
- `userId`: Foreign key to users
- `fileName`: Original file name
- `rawCsv`: CSV content
- `headers`: Column headers (JSON)
- `rowCount`: Number of data rows
- `columnCount`: Number of columns
- `createdAt`: Upload timestamp

**dataInsights**
- `id`: Primary key
- `datasetId`: Foreign key to csvDatasets
- `category`: Analysis category
- `insight`: Insight text
- `confidence`: Confidence score (0-100)
- `metadata`: Additional metadata (JSON)
- `createdAt`: Generation timestamp

**dataCleaningResults**
- `id`: Primary key
- `datasetId`: Foreign key to csvDatasets
- `cleanedCsv`: Cleaned CSV content
- `report`: Cleaning report (JSON)
- `createdAt`: Cleaning timestamp

## Deployment on Manus

### Prerequisites
- Manus account with API access
- Node.js 18+ and pnpm
- MySQL/TiDB database access
- Environment variables configured

### Environment Variables

```bash
# Database
DATABASE_URL=mysql://user:password@host:port/database

# Authentication
JWT_SECRET=your-jwt-secret
OAUTH_SERVER_URL=https://api.manus.im
VITE_OAUTH_PORTAL_URL=https://manus.im/login

# Manus Platform
VITE_APP_ID=your-app-id
VITE_APP_TITLE=Data Insights AI
VITE_APP_LOGO=https://your-domain.com/logo.png
OWNER_OPEN_ID=your-owner-id
OWNER_NAME=Your Name

# Built-in APIs
BUILT_IN_FORGE_API_URL=https://api.manus.im
BUILT_IN_FORGE_API_KEY=your-api-key

# Analytics (optional)
VITE_ANALYTICS_ENDPOINT=https://analytics.manus.im
VITE_ANALYTICS_WEBSITE_ID=your-website-id
```

### Deployment Steps

1. **Clone the Repository**
   ```bash
   git clone https://github.com/tomoto0/data-insights-ai.git
   cd data-insights-ai
   ```

2. **Install Dependencies**
   ```bash
   pnpm install
   ```

3. **Configure Environment**
   ```bash
   # Create .env file with required variables
   cp .env.example .env
   # Edit .env with your configuration
   ```

4. **Setup Database**
   ```bash
   # Push schema to database
   pnpm db:push
   ```

5. **Build Application**
   ```bash
   pnpm build
   ```

6. **Start Development Server**
   ```bash
   pnpm dev
   ```

7. **Deploy to Manus**
   - Use Manus Management UI
   - Connect GitHub repository
   - Configure environment variables
   - Deploy application

## API Documentation

### tRPC Procedures

#### CSV Management

**csv.upload** (Mutation)
- Input: `{ fileName: string, csvContent: string }`
- Output: `{ datasetId: number, rowCount: number, columnCount: number }`
- Description: Upload and parse CSV file

**csv.list** (Query)
- Output: `Array<{ id: number, fileName: string, rowCount: number, headers: string[], rawCsv: string }>`
- Description: List all datasets for current user

#### Insights

**insights.generate** (Mutation)
- Input: `{ datasetId: number, csvContent: string, headers: string[] }`
- Output: `{ success: boolean }`
- Description: Generate AI insights for dataset

**insights.list** (Query)
- Input: `{ datasetId: number }`
- Output: `Array<Insight>`
- Description: Retrieve insights for dataset

#### Data Cleaning

**cleaning.clean** (Mutation)
- Input: `{ datasetId: number, csvContent: string, headers: string[] }`
- Output: `{ cleanedCsv: string, report: CleaningReport }`
- Description: Clean and fix data quality issues

## Application Screenshots

![Data Insights AI - Landing Page](./01-12-202516.48の画像.jpeg)

*Landing page showing the professional interface with sign-in prompt and key features*

## Project Structure

```
data-insights-ai/
├── client/                          # Frontend application
│   ├── src/
│   │   ├── pages/
│   │   │   ├── Home.tsx            # Main application page
│   │   │   └── NotFound.tsx         # 404 page
│   │   ├── components/
│   │   │   ├── ui/                 # shadcn/ui components
│   │   │   ├── DashboardLayout.tsx # Layout component
│   │   │   └── ErrorBoundary.tsx   # Error handling
│   │   ├── contexts/               # React contexts
│   │   ├── hooks/                  # Custom hooks
│   │   ├── lib/
│   │   │   └── trpc.ts            # tRPC client configuration
│   │   ├── App.tsx                # Main app component
│   │   ├── main.tsx               # Entry point
│   │   └── index.css              # Global styles
│   ├── public/                     # Static assets
│   ├── index.html                 # HTML template
│   └── vite.config.ts             # Vite configuration
├── server/                         # Backend application
│   ├── routers.ts                 # tRPC router definitions
│   ├── db.ts                      # Database queries
│   ├── storage.ts                 # S3 storage helpers
│   ├── _core/
│   │   ├── index.ts              # Express server setup
│   │   ├── context.ts            # tRPC context
│   │   ├── trpc.ts               # tRPC configuration
│   │   ├── llm.ts                # Manus LLM integration
│   │   ├── imageGeneration.ts    # Image generation
│   │   ├── voiceTranscription.ts # Voice transcription
│   │   ├── notification.ts       # Notifications
│   │   ├── cookies.ts            # Cookie management
│   │   ├── env.ts                # Environment variables
│   │   └── systemRouter.ts       # System procedures
│   └── package.json
├── drizzle/                        # Database schema
│   ├── schema.ts                  # Table definitions
│   └── migrations/                # Database migrations
├── shared/                         # Shared types and constants
│   ├── const.ts                   # Constants
│   └── types.ts                   # Type definitions
├── package.json                   # Project dependencies
├── tsconfig.json                  # TypeScript configuration
├── tailwind.config.ts             # Tailwind CSS configuration
├── vite.config.ts                 # Vite configuration
└── README.md                       # This file
```

## Key Features Implementation

### 1. CSV Upload & Parsing
- Drag-and-drop file upload
- CSV parsing with header detection
- File size validation (max 10MB)
- Data preview before analysis

### 2. AI-Powered Analysis
- Multi-faceted analysis using Manus LLM
- 8 different analysis categories
- Confidence scoring for insights
- Category-based filtering
- Detailed recommendations

### 3. Data Cleaning
- Automatic issue detection
- Format standardization
- Missing value handling
- Column label improvement
- Before/after comparison
- CSV export functionality

### 4. Professional UI/UX
- Dark theme with gradient accents
- Responsive design
- Loading states and animations
- Error handling and user feedback
- Accessibility features
- Intuitive navigation

## Development

### Prerequisites
- Node.js 18+
- pnpm 8+
- MySQL 8+ or TiDB

### Setup
```bash
# Install dependencies
pnpm install

# Setup environment
cp .env.example .env

# Run database migrations
pnpm db:push

# Start development server
pnpm dev
```

### Build
```bash
# Build for production
pnpm build

# Preview production build
pnpm preview
```

### Testing
```bash
# Run tests
pnpm test

# Run tests in watch mode
pnpm test:watch
```

## Performance Considerations

- **Frontend**: Optimized React components with lazy loading
- **Backend**: Efficient database queries with Drizzle ORM
- **API**: tRPC for type-safe, minimal payload communication
- **Storage**: S3 for scalable file storage
- **Caching**: Query result caching for frequently accessed data

## Security

- **Authentication**: Manus OAuth integration
- **Authorization**: Role-based access control (RBAC)
- **Data Protection**: Encrypted database connections
- **API Security**: Protected tRPC procedures
- **Input Validation**: Comprehensive input validation
- **CORS**: Properly configured CORS headers

## Troubleshooting

### Common Issues

**Database Connection Error**
- Verify DATABASE_URL is correct
- Check database server is running
- Ensure user has proper permissions

**OAuth Errors**
- Verify VITE_APP_ID is correct
- Check OAUTH_SERVER_URL configuration
- Ensure redirect URLs are whitelisted

**CSV Upload Failures**
- Check file size (max 10MB)
- Verify CSV format is valid
- Ensure sufficient disk space

**LLM API Errors**
- Verify BUILT_IN_FORGE_API_KEY is valid
- Check API rate limits
- Ensure network connectivity

## Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Support

For support, issues, or questions:
- Open an issue on GitHub
- Contact the development team
- Check the documentation

## Acknowledgments

- Built with [Manus Platform](https://manus.im)
- Powered by OpenAI's LLM technology
- UI components from [shadcn/ui](https://ui.shadcn.com)
- Icons from [Lucide](https://lucide.dev)

## Version History

### v1.0.0 (2025-12-01)
- Initial release
- CSV upload and analysis
- AI-powered insights generation
- Data cleaning functionality
- Professional UI/UX
- Full Manus platform integration

---

**Last Updated**: December 1, 2025

**Repository**: [https://github.com/tomoto0/data-insights-ai](https://github.com/tomoto0/data-insights-ai)

**Live Demo**: [https://datainsights-erft3lrq.manus.space](https://datainsights-erft3lrq.manus.space)
