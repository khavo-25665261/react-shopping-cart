# React Shopping Cart - Project Overview

## 📋 Table of Contents
- [Introduction](#introduction)
- [Technology Stack](#technology-stack)
- [Project Architecture](#project-architecture)
- [Key Features](#key-features)
- [Project Structure](#project-structure)
- [State Management](#state-management)
- [Development Workflow](#development-workflow)
- [Testing](#testing)
- [Deployment](#deployment)

## Introduction

**React Shopping Cart** is a modern, production-ready e-commerce shopping cart application built with React and TypeScript. This project demonstrates best practices for building scalable, maintainable front-end applications with instant visual updates and a friendly user experience.

🔗 **Live Demo**: [https://react-shopping-cart-67954.firebaseapp.com/](https://react-shopping-cart-67954.firebaseapp.com/)

### Project Purpose
This application serves as a comprehensive example of how to:
- Build a responsive e-commerce interface with React
- Implement state management using React Context API and Hooks
- Use TypeScript for type-safe development
- Create styled components for maintainable CSS
- Implement a floating cart with real-time updates
- Filter products dynamically

## Technology Stack

### Core Technologies
- **React 18.0.0** - Modern React with concurrent features
- **TypeScript 4.6.3** - Static type checking for better code quality
- **Styled Components 5.3.3** - CSS-in-JS for component styling

### Build Tools & Development
- **React Scripts 5.0.0** - Built on Create React App
- **Node.js 14.17.3** - JavaScript runtime (specified in engines)
- **Axios 0.26.0** - HTTP client for API requests

### Testing
- **Jest** - Testing framework (via React Scripts)
- **@testing-library/react 13.0.0** - React component testing utilities
- **@testing-library/user-event 13.5.0** - User interaction simulation
- **@testing-library/react-hooks 7.0.2** - Custom hooks testing

### Code Quality & Formatting
- **ESLint** - Code linting (configured via React Scripts)
- **Prettier 2.5.1** - Code formatting
- **Husky 4.2.5** - Git hooks for quality checks
- **lint-staged 10.2.10** - Run linters on staged files
- **Commitlint** - Conventional commit message enforcement

### Deployment
- **Firebase Hosting** - Production deployment platform
- **CircleCI** - Continuous integration and deployment

## Project Architecture

### Component-Based Architecture
The application follows a component-based architecture with clear separation of concerns:

```
├── Components (UI Layer)
│   ├── App - Main application container
│   ├── Cart - Shopping cart sidebar
│   ├── Products - Product listing and display
│   ├── Filter - Product filtering by size
│   ├── Loader - Loading state component
│   └── Github/Recruiter - Additional UI elements
│
├── Contexts (State Management)
│   ├── cart-context - Cart state and operations
│   └── products-context - Product data and filtering
│
├── Services (Data Layer)
│   └── products.ts - Product data fetching
│
├── Models (Type Definitions)
│   └── TypeScript interfaces for type safety
│
└── Commons (Shared Resources)
    └── Styling utilities and themes
```

### Data Flow
1. **ProductsProvider** fetches and manages product data
2. **CartProvider** manages cart state (items, totals, visibility)
3. Components consume context via custom hooks
4. User interactions trigger context updates
5. UI automatically re-renders based on state changes

## Key Features

### 1. **Product Catalog**
- Display products with images, titles, descriptions, and pricing
- Show availability of different sizes
- Display free shipping indicator
- Show installment payment options

### 2. **Floating Shopping Cart**
- Sidebar cart that slides in/out
- Real-time cart updates
- Add/remove products with quantity tracking
- Calculate totals automatically
- Display installment information
- Persistent across product filtering

### 3. **Product Filtering**
- Filter products by available sizes (S, M, L, XL, etc.)
- Multiple size selection
- Real-time filtering with instant results
- Visual feedback for selected filters

### 4. **Responsive Design**
- Mobile-first approach
- Adapts to different screen sizes
- Touch-friendly interactions
- Optimized for tablets and desktops

### 5. **State Management with Context API**
- Centralized state management
- No prop drilling
- Custom hooks for easy context consumption
- Separation of concerns (cart vs products)

## Project Structure

```
react-shopping-cart/
│
├── public/                          # Static files
│   └── index.html                   # HTML template
│
├── src/
│   ├── components/                  # React components
│   │   ├── App/                     # Main app container
│   │   │   ├── App.tsx              # Component logic
│   │   │   ├── App.test.tsx         # Component tests
│   │   │   └── style.ts             # Styled components
│   │   │
│   │   ├── Cart/                    # Shopping cart
│   │   │   ├── CartProducts/        # Cart items list
│   │   │   └── Cart.tsx
│   │   │
│   │   ├── Products/                # Product listing
│   │   │   ├── Product/             # Individual product
│   │   │   └── Products.tsx
│   │   │
│   │   ├── Filter/                  # Size filter
│   │   ├── Loader/                  # Loading indicator
│   │   ├── Github/                  # GitHub corner/stars
│   │   └── Recruiter/               # Recruiter banner
│   │
│   ├── contexts/                    # React Context providers
│   │   ├── cart-context/
│   │   │   ├── CartContextProvider.tsx
│   │   │   ├── useCart.ts           # Cart operations hook
│   │   │   ├── useCartProducts.ts   # Cart products hook
│   │   │   └── useCartTotal.ts      # Cart total calculations
│   │   │
│   │   └── products-context/
│   │       ├── ProductsContextProvider.tsx
│   │       └── useProducts.tsx      # Products data hook
│   │
│   ├── models/                      # TypeScript interfaces
│   │   └── index.ts                 # IProduct, ICartProduct, etc.
│   │
│   ├── services/                    # API/data services
│   │   └── products.ts              # Product fetching logic
│   │
│   ├── commons/                     # Shared utilities
│   │   ├── Checkbox/                # Reusable checkbox
│   │   └── style/                   # Global styles, themes
│   │
│   ├── static/                      # Static JSON data
│   │   └── json/products.json       # Development product data
│   │
│   ├── utils/                       # Utility functions
│   │   └── formatPrice.ts           # Price formatting
│   │
│   ├── index.tsx                    # App entry point
│   └── setupTests.ts                # Test configuration
│
├── .circleci/                       # CI/CD configuration
├── .firebase/                       # Firebase config
├── package.json                     # Dependencies & scripts
├── tsconfig.json                    # TypeScript configuration
├── .prettierrc                      # Prettier config
├── .commitlintrc.js                 # Commit lint rules
└── README.md                        # Project README
```

## State Management

### Context Architecture

#### 1. Products Context
**Purpose**: Manage product catalog and filtering

**State**:
- `products` - Array of all products
- `filteredProducts` - Products matching selected filters
- `isFetching` - Loading state
- `selectedSizes` - Active size filters

**Operations**:
- `fetchProducts()` - Load products from API/JSON
- `filterProducts(sizes)` - Filter by size selection

**Hook**: `useProducts()`

#### 2. Cart Context
**Purpose**: Manage shopping cart state and operations

**State**:
- `isOpen` - Cart visibility (open/closed)
- `products` - Cart items with quantities
- `total` - Cart totals (quantity, price, installments)

**Operations** (via custom hooks):
- `addProduct(product)` - Add item to cart
- `removeProduct(product)` - Remove item from cart
- `increaseQuantity(product)` - Increase item quantity
- `decreaseQuantity(product)` - Decrease item quantity
- `calculateTotal()` - Recalculate cart totals

**Hooks**:
- `useCart()` - General cart operations
- `useCartProducts()` - Cart product management
- `useCartTotal()` - Total calculations

### Custom Hooks Pattern
The project uses custom hooks to encapsulate business logic:
- Cleaner component code
- Reusable logic
- Easier testing
- Better separation of concerns

## Development Workflow

### Getting Started

#### Prerequisites
```bash
Node.js 14.17.3
npm (comes with Node.js)
```

#### Installation
```bash
# Clone the repository
git clone https://github.com/khavo-25665261/react-shopping-cart.git

# Navigate to project directory
cd react-shopping-cart

# Install dependencies
npm install
```

#### Development Server
```bash
# Start development server (runs on http://localhost:3000)
npm start
```

#### Building for Production
```bash
# Create optimized production build
npm run build
```

### Available Scripts

| Command | Description |
|---------|-------------|
| `npm start` | Start development server with hot reload |
| `npm run build` | Create production build |
| `npm test` | Run tests in watch mode (silent) |
| `npm run test:watch` | Run tests in interactive watch mode |
| `npm run test:coverage` | Generate test coverage report |
| `npm run lint` | Lint source code with ESLint |
| `npm run format` | Format code with Prettier |
| `npm run deploy` | Deploy to Firebase hosting |
| `npm run eject` | Eject from Create React App (irreversible) |

### Code Quality Tools

#### Pre-commit Hooks
The project uses Husky to enforce quality checks:
- **Commit Message Linting**: Ensures conventional commit format
- **Code Formatting**: Auto-formats staged files with Prettier
- **Linting**: Runs ESLint on JavaScript/TypeScript files

#### Conventional Commits
Commit messages must follow the format:
```
type(scope): subject

Examples:
feat(cart): add product quantity selector
fix(filter): correct size filtering logic
docs(readme): update installation instructions
```

## Testing

### Testing Strategy
The project maintains high test coverage with the following standards:

**Coverage Thresholds**:
- **Branches**: 64%
- **Functions**: 90%
- **Lines**: 90%
- **Statements**: 90%

### Test Structure
Tests are co-located with components in `__tests__` directories or as `*.test.tsx` files:

```
Component/
├── Component.tsx
├── Component.test.tsx
└── __tests__/
    └── integration.test.tsx
```

### Testing Libraries
- **Jest**: Test runner and assertion library
- **React Testing Library**: Component testing utilities
- **React Hooks Testing Library**: For testing custom hooks
- **User Event**: Simulating user interactions

### Running Tests
```bash
# Run all tests
npm test

# Run tests with coverage
npm run test:coverage

# Run tests in watch mode
npm run test:watch
```

### Test Examples
The project includes tests for:
- Component rendering
- User interactions (clicking, typing)
- Context providers and hooks
- Utility functions
- Snapshot testing for UI consistency

## Deployment

### Firebase Hosting
The application is deployed to Firebase Hosting with the following setup:

**Configuration Files**:
- `.firebaserc` - Firebase project configuration
- `firebase.json` - Hosting rules and settings

**Deployment Process**:
```bash
# Build production bundle
npm run build

# Deploy to Firebase
npm run deploy
```

### Continuous Integration (CircleCI)
The project uses CircleCI for automated testing and deployment:

**CI Pipeline**:
1. Install dependencies
2. Run linting
3. Run tests
4. Build production bundle
5. Deploy to Firebase (on main branch)

**Configuration**: `.circleci/config.yml`

### Environment Handling
The application adapts based on `NODE_ENV`:
- **Development**: Uses local JSON data (`static/json/products.json`)
- **Production**: Fetches data from Firebase Realtime Database

## Data Models

### Product Interface
```typescript
interface IProduct {
  id: number;
  sku: number;
  title: string;
  description: string;
  availableSizes: string[];
  style: string;
  price: number;
  installments: number;
  currencyId: string;
  currencyFormat: string;
  isFreeShipping: boolean;
}
```

### Cart Product Interface
```typescript
interface ICartProduct extends IProduct {
  quantity: number;  // Added for cart management
}
```

### Cart Total Interface
```typescript
interface ICartTotal {
  productQuantity: number;
  installments: number;
  totalPrice: number;
  currencyId: string;
  currencyFormat: string;
}
```

## Best Practices Demonstrated

1. **TypeScript Integration**: Full type safety across the application
2. **Component Composition**: Small, reusable, single-responsibility components
3. **Custom Hooks**: Encapsulated business logic
4. **Context API**: Proper state management without prop drilling
5. **Styled Components**: Scoped CSS with theming support
6. **Testing**: Comprehensive test coverage
7. **Code Quality**: Automated linting and formatting
8. **Conventional Commits**: Standardized commit messages
9. **Responsive Design**: Mobile-first approach
10. **Performance**: React 18 with concurrent features

## Contributing Guidelines

Based on the project structure and tooling, contributors should follow these best practices:
- Use TypeScript for all new code
- Follow existing code style (enforced by Prettier)
- Write tests for new features
- Use conventional commit messages (enforced by commitlint)
- Ensure all tests pass before committing
- Maintain or improve test coverage thresholds

## License

The MIT License (MIT) - As specified in the README.md

## Credits

- **Original Author**: Jefferson Ribeiro
- **Original Repository**: https://github.com/jeffersonRibeiro/react-shopping-cart
- **Current Fork**: https://github.com/khavo-25665261/react-shopping-cart

---

*This project serves as an excellent learning resource for modern React development practices and can be used as a foundation for building production e-commerce applications.*
