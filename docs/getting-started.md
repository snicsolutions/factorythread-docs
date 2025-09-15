---
layout: default
title: Getting Started
nav_order: 2
---

# Getting Started
{: .no_toc }

This guide will help you get up and running with Factory Thread quickly and efficiently.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Prerequisites

Before you begin, ensure you have the following installed on your system:

- **Node.js** (version 16 or higher)
- **npm** or **yarn** package manager
- **Git** for version control
- A modern web browser for testing

## Installation

### Step 1: Install Factory Thread

```bash
npm install -g factory-thread
```

Or using yarn:

```bash
yarn global add factory-thread
```

### Step 2: Verify Installation

Confirm that Factory Thread is installed correctly:

```bash
factory-thread --version
```

You should see the version number displayed in your terminal.

## Quick Start

### Create Your First Project

1. **Initialize a new project**:
   ```bash
   factory-thread init my-project
   cd my-project
   ```

2. **Install dependencies**:
   ```bash
   npm install
   ```

3. **Start the development server**:
   ```bash
   npm run dev
   ```

4. **Open your browser** and navigate to `http://localhost:3000`

## Project Structure

Your new Factory Thread project includes:

```
my-project/
├── src/                 # Source code
│   ├── components/      # Reusable components
│   ├── pages/          # Application pages
│   └── utils/          # Utility functions
├── public/             # Static assets
├── package.json        # Project dependencies
└── factory.config.js   # Factory Thread configuration
```

## Configuration

Factory Thread uses a configuration file (`factory.config.js`) to customize your development environment:

```javascript
module.exports = {
  // Development server settings
  server: {
    port: 3000,
    host: 'localhost'
  },
  
  // Build settings
  build: {
    outputDir: 'dist',
    sourceMaps: true
  },
  
  // Feature flags
  features: {
    hotReload: true,
    autoRefresh: true
  }
};
```

## Next Steps

Now that you have Factory Thread up and running:

1. [Explore the Features]({{ site.baseurl }}{% link docs/features.md %}) - Learn about Factory Thread's powerful capabilities
2. [API Reference]({{ site.baseurl }}{% link docs/api-reference.md %}) - Dive into the technical details

## Getting Help

If you encounter any issues:

- Browse existing [GitHub Issues](https://github.com/snicsolutions/factorythread/issues)
- Create a new issue if you can't find a solution