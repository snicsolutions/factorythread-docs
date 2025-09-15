---
layout: default
title: API Reference
nav_order: 4
---

# API Reference
{: .no_toc }

Complete reference for Factory Thread APIs and configuration options.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Core API

### factoryThread.init(config)

Initialize a new Factory Thread application.

**Parameters:**
- `config` (Object): Configuration object

**Returns:** Promise<Application>

**Example:**
```javascript
import factoryThread from 'factory-thread';

const app = await factoryThread.init({
  name: 'my-app',
  version: '1.0.0',
  environment: 'development'
});
```

### factoryThread.createClient(options)

Create an HTTP client with built-in retry and caching.

**Parameters:**
- `options` (Object): Client configuration
  - `baseURL` (string): Base URL for all requests
  - `timeout` (number): Request timeout in milliseconds
  - `retries` (number): Number of retry attempts
  - `cache` (boolean): Enable response caching

**Returns:** HttpClient

**Example:**
```javascript
const client = factoryThread.createClient({
  baseURL: 'https://api.example.com',
  timeout: 5000,
  retries: 3,
  cache: true
});

const response = await client.get('/users');
```

## Configuration API

### Application Configuration

Configure your Factory Thread application using `factory.config.js`:

```javascript
module.exports = {
  // Application settings
  app: {
    name: 'My Application',
    version: '1.0.0',
    description: 'My Factory Thread application'
  },
  
  // Server configuration
  server: {
    port: process.env.PORT || 3000,
    host: process.env.HOST || 'localhost',
    cors: {
      origin: ['http://localhost:3000'],
      credentials: true
    }
  },
  
  // Database configuration
  database: {
    type: 'postgresql',
    host: process.env.DB_HOST,
    port: process.env.DB_PORT,
    username: process.env.DB_USERNAME,
    password: process.env.DB_PASSWORD,
    database: process.env.DB_NAME
  },
  
  // Build settings
  build: {
    outputDir: 'dist',
    sourceMaps: true,
    minify: process.env.NODE_ENV === 'production',
    optimization: {
      splitChunks: true,
      treeshaking: true
    }
  },
  
  // Feature flags
  features: {
    hotReload: process.env.NODE_ENV === 'development',
    autoRefresh: true,
    typeChecking: true
  }
};
```

## Database API

### Model Definition

Define database models with TypeScript support:

```typescript
import { Model, Column, Table, DataType } from '@factory-thread/database';

@Table({
  tableName: 'users',
  timestamps: true
})
export class User extends Model {
  @Column({
    type: DataType.UUID,
    primaryKey: true,
    defaultValue: DataType.UUIDV4
  })
  id: string;

  @Column({
    type: DataType.STRING,
    allowNull: false,
    unique: true
  })
  email: string;

  @Column({
    type: DataType.STRING,
    allowNull: false
  })
  name: string;

  @Column({
    type: DataType.DATE,
    allowNull: true
  })
  lastLoginAt: Date;
}
```

### Database Operations

```typescript
// Create
const user = await User.create({
  email: 'user@example.com',
  name: 'John Doe'
});

// Read
const users = await User.findAll({
  where: {
    lastLoginAt: {
      [Op.gte]: new Date(Date.now() - 30 * 24 * 60 * 60 * 1000) // Last 30 days
    }
  },
  order: [['lastLoginAt', 'DESC']],
  limit: 10
});

// Update
await User.update(
  { lastLoginAt: new Date() },
  { where: { id: userId } }
);

// Delete
await User.destroy({
  where: { id: userId }
});
```

## Authentication API

### Auth Configuration

```javascript
// factory.config.js
module.exports = {
  auth: {
    provider: 'jwt',
    secret: process.env.JWT_SECRET,
    expiresIn: '7d',
    refreshToken: {
      enabled: true,
      expiresIn: '30d'
    },
    providers: {
      google: {
        clientId: process.env.GOOGLE_CLIENT_ID,
        clientSecret: process.env.GOOGLE_CLIENT_SECRET
      }
    }
  }
};
```

### Authentication Methods

```typescript
import { auth } from '@factory-thread/auth';

// Login with email and password
const result = await auth.login({
  email: 'user@example.com',
  password: 'password123'
});

// OAuth login
const googleUser = await auth.loginWithProvider('google', {
  code: authorizationCode
});

// Get current user
const currentUser = await auth.getCurrentUser();

// Logout
await auth.logout();

// Refresh token
const newTokens = await auth.refreshToken(refreshToken);
```

## Testing API

### Test Utilities

```typescript
import { createTestApp, createTestClient } from '@factory-thread/testing';

describe('User API', () => {
  let app;
  let client;

  beforeAll(async () => {
    app = await createTestApp({
      database: ':memory:' // Use in-memory database for tests
    });
    client = createTestClient(app);
  });

  afterAll(async () => {
    await app.close();
  });

  test('should create a new user', async () => {
    const response = await client
      .post('/api/users')
      .send({
        email: 'test@example.com',
        name: 'Test User'
      })
      .expect(201);

    expect(response.body).toMatchObject({
      email: 'test@example.com',
      name: 'Test User'
    });
  });
});
```

## Deployment API

### Build Commands

```bash
# Development build
factory-thread build --env development

# Production build
factory-thread build --env production

# Build with analysis
factory-thread build --analyze

# Build and deploy
factory-thread deploy --target production
```

### Deployment Configuration

```javascript
// factory.config.js
module.exports = {
  deployment: {
    targets: {
      staging: {
        provider: 'aws',
        region: 'us-east-1',
        bucket: 'my-app-staging',
        cloudfront: true
      },
      production: {
        provider: 'aws',
        region: 'us-east-1',
        bucket: 'my-app-production',
        cloudfront: true,
        environment: {
          NODE_ENV: 'production',
          API_URL: 'https://api.myapp.com'
        }
      }
    }
  }
};
```

## Error Handling

### Global Error Handler

```typescript
import { ErrorHandler } from '@factory-thread/core';

// Custom error handler
const errorHandler = new ErrorHandler({
  logErrors: true,
  showStackTrace: process.env.NODE_ENV === 'development'
});

// Handle specific error types
errorHandler.handle('ValidationError', (error, req, res) => {
  res.status(400).json({
    error: 'Validation failed',
    details: error.details
  });
});

// Handle all other errors
errorHandler.handleAll((error, req, res) => {
  console.error('Unhandled error:', error);
  res.status(500).json({
    error: 'Internal server error'
  });
});
```

## Type Definitions

Factory Thread provides comprehensive TypeScript definitions for all APIs. Import types as needed:

```typescript
import {
  Application,
  Configuration,
  DatabaseConfig,
  AuthConfig,
  HttpClient,
  Model,
  User
} from 'factory-thread';
```