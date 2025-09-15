# Factory Thread Documentation

This repository contains the official documentation for Factory Thread, built with Jekyll and the Just the Docs theme for GitHub Pages.

## 🌐 Live Site

Visit the documentation at: [https://yourusername.github.io/factorythread-docs](https://yourusername.github.io/factorythread-docs)

## 🛠 Local Development

### Prerequisites

- Ruby (version 2.7 or higher)
- Bundler gem

### Setup

1. Clone this repository:
   ```bash
   git clone https://github.com/yourusername/factorythread-docs.git
   cd factorythread-docs
   ```

2. Install dependencies:
   ```bash
   bundle install
   ```

3. Run the local server:
   ```bash
   bundle exec jekyll serve
   ```

4. Open your browser and navigate to `http://localhost:4000/factorythread-docs`

## 📝 Contributing

### Adding New Documentation

1. Create a new markdown file in the `docs/` directory
2. Add the appropriate front matter:
   ```yaml
   ---
   layout: default
   title: Your Page Title
   nav_order: 5
   ---
   ```
3. Write your content using markdown
4. Commit and push your changes

### Editing Existing Pages

Simply edit the markdown files and push your changes. The site will automatically rebuild and deploy via GitHub Actions.

## 📁 Project Structure

```
factorythread-docs/
├── _config.yml                    # Jekyll configuration
├── Gemfile                        # Ruby dependencies
├── index.md                       # Homepage
├── .github/workflows/pages.yml    # GitHub Pages deployment workflow
└── docs/
    ├── getting-started.md          # Installation guide
    ├── features.md                 # Feature overview
    └── api-reference.md            # API documentation
```

## ⚙️ Configuration

The site is configured using Jekyll with the Just the Docs theme. Key configuration options are in `_config.yml`:

- **Theme**: Uses the `just-the-docs` remote theme
- **Search**: Enabled with customizable settings
- **Navigation**: Automatic navigation generation
- **GitHub Integration**: Edit links and repository information

## 🚀 Deployment

This site uses GitHub Actions for automatic deployment to GitHub Pages. The workflow:

1. Triggers on pushes to the `main` branch
2. Builds the Jekyll site
3. Deploys to GitHub Pages

No manual deployment steps are required.

## 📄 License

This documentation is distributed under the MIT License. See `LICENSE` for more information.

## 🤝 Support

For issues or questions about the documentation:

1. Check existing [GitHub Issues](https://github.com/yourusername/factorythread-docs/issues)
2. Create a new issue if needed
3. For Factory Thread product support, visit the main repository
