# Next.js Routing & Data Fetching

A comprehensive Next.js application demonstrating advanced routing patterns and server-side data fetching techniques using the App Router. This project showcases modern Next.js 16.2 features including dynamic routes, parallel routes, intercepted routes, and real-time data fetching.

## 🎯 Project Overview

This project is a **news management application** that demonstrates:

- **App Router Architecture** - Modern file-based routing with semantic directory organization
- **Server-Side Data Fetching** - Using async server components with REST API integration
- **Dynamic Routes** - Parameter-based routing for individual news articles
- **Parallel Routes (Slots)** - Rendering multiple segments simultaneously at the same level
- **Intercepted Routes** - Capturing and redirecting routes while maintaining URL consistency
- **Route Groups** - Organizing code without affecting URL structure
- **Catch-All Routes** - Flexible routing patterns for complex navigation

## 🛠️ Tech Stack

- **Framework**: [Next.js](https://nextjs.org) 16.2.9 (App Router)
- **Frontend**: React 19.2.4 with TypeScript
- **Styling**: Tailwind CSS 4 with PostCSS
- **Database**: SQLite3 (better-sqlite3)
- **Backend**: Express.js with CORS
- **Language**: TypeScript (72.4%) | JavaScript (14.4%) | CSS (13.2%)

## 📂 Project Structure

```
├── app/                              # Next.js App Router
│   └── (content)/                   # Route group - doesn't affect URL
│       ├── news/                    # News listing pages
│       │   ├── page.tsx            # Main news page (fetches from backend)
│       │   └── [slug]/             # Dynamic route for individual articles
│       │       ├── page.tsx        # Article detail page
│       │       ├── image/          # Image display page
│       │       │   └── page.tsx
│       │       └── @modal/         # Parallel route for modal
│       │           └── (.)image/   # Intercepted route for modal image
│       │               └── page.tsx
│       ├── archive/                # News archive by year and month
│       │   ├── @archive/           # Parallel route slot
│       │   │   ├── page.tsx        # Archive index
│       │   │   └── [year]/         # Dynamic year route
│       │   │       └── page.tsx
│       │   └── @latest/            # Parallel route slot
│       │       └── default.tsx     # Latest news display
│       └── stories/                # Catch-all route
│           └── [[...filter]]/      # Optional catch-all params
│               └── page.tsx        # News with advanced filtering
├── components/                      # Reusable React components
│   ├── newsList.tsx               # News list renderer
│   └── modalBackdrop.tsx           # Modal backdrop component
├── utils/                          # Server-side utilities
│   └── news.ts                    # Data fetching utilities
├── public/                         # Static assets
│   └── images/news/               # News images
├── backend/                        # Express.js backend
│   ├── app.js                     # Express server setup
│   └── package.json               # Backend dependencies
├── package.json                    # Frontend dependencies
└── README.md                       # Project documentation
```

## 🚀 Key Features

### 1. **Dynamic Routing with Parameters**
- `/news/[slug]` - Individual news article pages
- `/archive/[year]` - News archived by year
- `/stories/[[...filter]]` - Flexible multi-level filtering for year and month

### 2. **Parallel Routes (Slots)**
- `@archive` and `@latest` slots on the archive page
- Enables rendering multiple segments at the same URL level
- Reduces code duplication through shared layouts

### 3. **Intercepted Routes**
- `(.)image` interceptor for modal dialogs
- Captures `/news/[slug]/image` requests to display in a modal
- Maintains clean URL structure while changing rendered content

### 4. **Server-Side Data Fetching**
- Async server components with built-in data fetching
- RESTful API integration (`http://localhost:8080/news`)
- Automatic cache management and revalidation

### 5. **Route Groups**
- `(content)` folder organizes related routes
- Doesn't affect the URL structure
- Improves code organization and maintainability

### 6. **Error Handling**
- `notFound()` redirects for missing articles
- Error boundaries for failed data fetches
- Graceful fallbacks for unavailable content

## 🗄️ Data Structure

The application fetches news data from the backend with the following structure:

```typescript
interface NEWS {
  slug: string;      // Unique identifier for the article
  title: string;     // Article title
  content: string;   // Article body
  date: string;      // Publication date (YYYY-MM-DD format)
  image: string;     // Image filename in /public/images/news/
}
```

## 🏃 Getting Started

### Prerequisites
- Node.js 18+ (Frontend)
- Node.js 14+ (Backend)
- npm, yarn, pnpm, or bun

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/princekakkar34/next-routing_and_data-fetching.git
   cd next-routing_and_data-fetching
   ```

2. **Install frontend dependencies**
   ```bash
   npm install
   # or
   yarn install
   # or
   pnpm install
   # or
   bun install
   ```

3. **Install backend dependencies**
   ```bash
   cd backend
   npm install
   cd ..
   ```

### Running the Application

1. **Start the backend server** (in one terminal)
   ```bash
   cd backend
   npm start
   ```
   The backend will run on `http://localhost:8080`

2. **Start the frontend development server** (in another terminal)
   ```bash
   npm run dev
   # or
   yarn dev
   # or
   pnpm dev
   # or
   bun dev
   ```
   The frontend will be available at `http://localhost:3000`

3. **Open your browser**
   - Navigate to [http://localhost:3000](http://localhost:3000)
   - Browse the news articles and explore the different routing patterns

### Available Scripts

**Frontend:**
- `npm run dev` - Start development server with hot reload
- `npm run build` - Build for production
- `npm start` - Start production server
- `npm run lint` - Run ESLint

**Backend:**
- `npm start` - Start Express server on port 8080

## 📚 Learning Resources

### Next.js Routing Concepts Demonstrated

- [App Router Documentation](https://nextjs.org/docs/app) - File-based routing system
- [Dynamic Routes](https://nextjs.org/docs/app/building-your-application/routing/dynamic-routes) - Handle variable URLs
- [Parallel Routes](https://nextjs.org/docs/app/building-your-application/routing/parallel-routes) - Render multiple segments simultaneously
- [Intercepted Routes](https://nextjs.org/docs/app/building-your-application/routing/intercepting-routes) - Intercept and re-route requests
- [Route Groups](https://nextjs.org/docs/app/building-your-application/routing/route-groups) - Organize routes without URL impact
- [Server Components](https://nextjs.org/docs/app/building-your-application/rendering/server-components) - Render on the server
- [Data Fetching](https://nextjs.org/docs/app/building-your-application/data-fetching) - Fetch data in server components

### External Resources

- [Next.js Official Documentation](https://nextjs.org/docs)
- [React Documentation](https://react.dev)
- [TypeScript Handbook](https://www.typescriptlang.org/docs)
- [Tailwind CSS Documentation](https://tailwindcss.com/docs)

## 🔧 Configuration

### Environment Variables

Currently, the backend URL is hardcoded as `http://localhost:8080/news`. For production use, consider:

```typescript
// .env.local
NEXT_PUBLIC_API_URL=http://localhost:8080
```

Then use in components:
```typescript
const response = await fetch(`${process.env.NEXT_PUBLIC_API_URL}/news`);
```

## 📖 Example Usage

### Accessing Different Routes

- **News Home**: `/news` - Lists all news articles
- **Article Detail**: `/news/article-slug` - View specific article
- **Article Image**: `/news/article-slug/image` - Full-screen image
- **Article Modal**: Click image link (intercepted modal view)
- **Archive**: `/archive` - Browse news by year and month
- **Stories**: `/stories` - Browse with advanced filtering
- **Filtered Stories**: `/stories/2024` or `/stories/2024/03` - Year or month-specific

## 🎓 What You'll Learn

This project is ideal for developers learning:

1. **Next.js App Router** - Modern routing with semantic folder structures
2. **Advanced Route Patterns** - Dynamic, parallel, and intercepted routes
3. **Server Components** - Efficient server-side rendering and data fetching
4. **TypeScript in React** - Type-safe component development
5. **REST API Integration** - Connecting frontend and backend applications
6. **Project Organization** - Structuring larger Next.js applications

## 📝 Notes

- This is an educational project demonstrating Next.js routing patterns
- The backend uses SQLite for simplicity; upgrade to PostgreSQL for production
- Images should be placed in `/public/images/news/` directory
- Ensure backend is running before starting the frontend development server

## 📄 License

This project is open source and available under the ISC License.

## 👤 Author

[Prince Kakkar](https://github.com/princekakkar34)

---

**Happy Learning!** 🎉 Explore the code and experiment with different routing patterns to deepen your understanding of modern Next.js applications.
